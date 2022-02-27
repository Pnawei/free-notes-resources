---
title: Java 8新特性
date: 2021-11-15
tags: 
    - 新日期时间
    - Lambda
    - Java
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。 

- 视频资料：宋红康 – 全网最全Java零基础入门教程：https://www.bilibili.com/video/BV1Kb411W75N（只看 Java 8 部分即可）
- 文档：菜鸟教程  https://www.runoob.com/java/java-tutorial.html
- 书籍：《Java 8 实战》

<!-- more -->

### Lambda 表达式

- lambda 表达式的语法格式：

  ```java
  /*以下是lambda表达式的重要特征:
  
  1.可选类型声明：不需要声明参数类型，编译器可以统一识别参数值。
  2.可选的参数圆括号：一个参数无需定义圆括号，但多个参数需要定义圆括号。
  3.可选的大括号：如果主体包含了一个语句，就不需要使用大括号。
  4.可选的返回关键字：如果主体只有一个表达式返回值则编译器会自动返回值，大括号需要指定表达式返回了一个数值。
  */
  
  (parameters) -> expression
  或
  (parameters) ->{ statements; }
  ```

- lambda 简单实例

  ```java
  // 1. 不需要参数,返回值为 5  
  () -> 5  
    
  // 2. 接收一个参数(数字类型),返回其2倍的值  
  x -> 2 * x  
    
  // 3. 接受2个参数(数字),并返回他们的差值  
  (x, y) -> x – y  
    
  // 4. 接收2个int型整数,返回他们的和  
  (int x, int y) -> x + y  
    
  // 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
  (String s) -> System.out.print(s)
  ```

- java 8 中代码实例

  ```java
  public class Java8Tester {
     public static void main(String args[]){
        Java8Tester tester = new Java8Tester();
          
        // 类型声明
        MathOperation addition = (int a, int b) -> a + b;
          
        // 不用类型声明
        MathOperation subtraction = (a, b) -> a - b;
          
        // 大括号中的返回语句
        MathOperation multiplication = (int a, int b) -> { return a * b; };
          
        // 没有大括号及返回语句
        MathOperation division = (int a, int b) -> a / b;
          
        System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
        System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
        System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
        System.out.println("10 / 5 = " + tester.operate(10, 5, division));
          
        // 不用括号
        GreetingService greetService1 = message ->
        System.out.println("Hello " + message);
          
        // 用括号
        GreetingService greetService2 = (message) ->
        System.out.println("Hello " + message);
          
        greetService1.sayMessage("Runoob");
        greetService2.sayMessage("Google");
     }
      
     interface MathOperation {
        int operation(int a, int b);
     }
      
     interface GreetingService {
        void sayMessage(String message);
     }
      
     private int operate(int a, int b, MathOperation mathOperation){
        return mathOperation.operation(a, b);
     }
  }
  ```

  

#### 新日期时间 API  【Local（本地）和Zoned（时区）】

- Local（本地）实例

  ```java
  /*  Java8Tester1.java 文件 */
  
  import java.time.LocalDate;
  import java.time.LocalTime;
  import java.time.LocalDateTime;
  import java.time.Month;
   
  public class Java8Tester1 {
     public static void main(String args[]){
        Java8Tester java8tester = new Java8Tester();
        java8tester.testLocalDateTime();
     }
      
     public void testLocalDateTime(){
      
        // 获取当前的日期时间
        LocalDateTime currentTime = LocalDateTime.now();
        System.out.println("当前时间: " + currentTime);
          
        LocalDate date1 = currentTime.toLocalDate();
        System.out.println("date1: " + date1);
          
        Month month = currentTime.getMonth();
        int day = currentTime.getDayOfMonth();
        int seconds = currentTime.getSecond();
          
        System.out.println("月: " + month +", 日: " + day +", 秒: " + seconds);
          
        LocalDateTime date2 = currentTime.withDayOfMonth(10).withYear(2012);
        System.out.println("date2: " + date2);
          
        // 12 december 2014
        LocalDate date3 = LocalDate.of(2014, Month.DECEMBER, 12);
        System.out.println("date3: " + date3);
          
        // 22 小时 15 分钟
        LocalTime date4 = LocalTime.of(22, 15);
        System.out.println("date4: " + date4);
          
        // 解析字符串
        LocalTime date5 = LocalTime.parse("20:15:30");
        System.out.println("date5: " + date5);
     }
  }
  
  
  /*输出结果：
  当前时间: 2016-04-15T16:55:48.668
  date1: 2016-04-15
  月: APRIL, 日: 15, 秒: 48
  date2: 2012-04-10T16:55:48.668
  date3: 2014-12-12
  date4: 22:15
  date5: 20:15:30
  */
  ```
  
- Zoned（时区）实例

  ```java
  /* Java8Tester2.java 文件 */
  
  import java.time.ZonedDateTime;
  import java.time.ZoneId;
   
  public class Java8Tester2 {
     public static void main(String args[]){
        Java8Tester java8tester = new Java8Tester();
        java8tester.testZonedDateTime();
     }
      
     public void testZonedDateTime(){
      
        // 获取当前时间日期
        ZonedDateTime date1 = ZonedDateTime.parse("2015-12-03T10:15:30+05:30[Asia/Shanghai]");
        System.out.println("date1: " + date1);
          
        ZoneId id = ZoneId.of("Europe/Paris");
        System.out.println("ZoneId: " + id);
          
        ZoneId currentZone = ZoneId.systemDefault();
        System.out.println("当期时区: " + currentZone);
     }
  }
  
  /*输出结果：
  date1: 2015-12-03T10:15:30+08:00[Asia/Shanghai]
  ZoneId: Europe/Paris
  当期时区: Asia/Shanghai
  
  */
  ```

  

#### 接口默认方法

- 什么是默认方法？

  `简单说，默认方法就是接口可以有实现方法，而且不需要实现类去实现其方法。我们只需在方法名前面加个 default 关键字即可实现默认方法。`

- 多个默认方法

  - 实例：

    ```java
    public interface Vehicle {
       default void print(){
          System.out.println("我是一辆车!");
       }
    }
     
    public interface FourWheeler {
       default void print(){
          System.out.println("我是一辆四轮车!");
       }
    }
    ```

  - 第一个解决方案是创建自己的默认方法，来覆盖重写接口的默认方法：

    ```java
    public class Car implements Vehicle, FourWheeler {
       default void print(){
          System.out.println("我是一辆四轮汽车!");
       }
    }
    ```

  - 第二种解决方案可以使用 super 来调用指定接口的默认方法：

    ```java
    public class Car implements Vehicle, FourWheeler {
       public void print(){
          Vehicle.super.print();
       }
    }
    ```

- 实例

  ```java
  public class Java8Tester {
     public static void main(String args[]){
        Vehicle vehicle = new Car();
        vehicle.print();
     }
  }
   
  interface Vehicle {
     default void print(){
        System.out.println("我是一辆车!");
     }
     //Java 8 的另一个特性是接口可以声明（并且可以提供实现）静态方法
     static void blowHorn(){
        System.out.println("按喇叭!!!");
     }
  }
  
  interface FourWheeler {
     default void print(){
        System.out.println("我是一辆四轮车!");
     }
  }
   
  class Car implements Vehicle, FourWheeler {
     public void print(){
        Vehicle.super.print();
        FourWheeler.super.print();
        Vehicle.blowHorn();
        System.out.println("我是一辆汽车!");
     }
  }
  
  
  /*输出结果：
  我是一辆车!
  我是一辆四轮车!
  按喇叭!!!
  我是一辆汽车!
  
  */
  ```

  