---
title: Java入门
date: 2021-11-01
tags: 
    - 入门
    - 知识
    - Java
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。 

- 视频资料：韩顺平|零基础30天学Java  https://www.bilibili.com/video/BV1fh411y7R8
- 文档：菜鸟教程  https://www.runoob.com/java/java-tutorial.html
- 书籍：

<!-- more -->

# Java基础知识

## Java特性

```java
1.简单（不是使用指针，而是引用）
2.面向对象、分布式（类库和接口）
3.健壮性（异常处理）
4.安全性（安全防范机制：类ClassLoader 和提供安全管理机制：类 SecurityManager）
```

## Java开发环境 

**了解java虚拟机jvm，会jdk的安装 及 集成开发环境 IntelliJ IDEA 的使用**  （Eclipse 菜鸟教程有教程）

**快速生成语句** 

- 快速生成main()方法： psvm 回车 /  直接敲main智能提示
- 快速生成输出语句： sout 回车             输出语句为：System.out.println();

 **内容辅助键**

- Ctrl+Alt+space(内容提示，代码补全等)

**常用快捷键**

- 注释：

​		单行：Ctrl + /

​		多行：Ctrl + Shift + /

- 代码格式化： Ctrl + Alt + L


- IDEA中生成构造函数： Atl + Insert   

- 查看继承情况：Ctrl + B 

- 集合遍历快捷键  集合对象名.fori （或对象.for）---->  //foreach的

- 方法自动定位类  Ctrl + B

- 更改模板快捷键       file -> settings -> editor -> Live templates ->

  查看有哪些模板快捷键/可以自己增加模板

  模板可以高效的完成开发

- 代码补全   Alt + /

- 显示所有快捷键的快捷键  ctrl + j 

## 基础语法

### 数据类型

#### 变量

- 局部变量 ：类方法中的变量
- 类变量：（静态变量）独立于方法之外的变量 
- 实例变量：（全局变量）独立于方法之外的变量，不过没有 static 修饰

#### **修饰符**

- 访问控制修饰符 : default（默认）, public , protected, private

  | 访问级别 | 访问控制修饰符 | 同类 | 同包 | 子类 | 不同包 |
  | :------: | :------------: | :--: | :--: | :--: | :----: |
  |   公开   |     public     |  √   |  √   |  √   |   √    |
  |  受保护  |   protected    |  √   |  √   |  √   |   ×    |
  |   默认   |   没有修饰符   |  √   |  √   |  ×   |   ×    |
  |   私有   |    private     |  √   |  ×   |  ×   |   ×    |

- 非访问控制修饰符 : final, abstract, static, synchronized

#### **关键字**  

​	 注意：在进行命名的时候不能使用关键字。一旦使用了关键字，将会造成命名冲突。

- final关键字

  可以修饰类、属性、方法和局部变量

  ```
  使用final的几种情况
  当不希望类被继承时，可以用final修饰
  当不希望父类的某个方法被子类覆盖/重写(override)时，可以用final关键字修饰
  当不希望类的某个属性的值被修改，可以用final修饰
  当不希望某个局部变量被修改，可以用final修饰
  
  ```

- 使用细节1

  ```java
  class AA {
      /*
       *1 定义时：如 public final double TAX_RATE = 8.0
       *2 在构造器中
       *3 在代码块中
       * */
      public final double TAX_RATE = 8.0; //定义时赋值
      public final double TAX_RATE2;
      public final double TAX_RATE3;
  
      public AA() {//构造器中赋值
          TAX_RATE2 = 2.2;
      }
      
      {//代码块中赋值
          TAX_RATE3 = 3.5;
      }
  }
  
  ```

- 使用细节2

  ```java
  class BB {
      /*
     如果final 修饰的属性时静态的，则初始化的位置只能是
     1 定义时  2 在静态代码块中  不能在构造器中赋值。
       * */
      public static final double TAX_RATE = 8.0; //定义时赋值
      //public static final double TAX_RATE2;
      public static final double TAX_RATE3;
  
  //    public AA() {//构造器中赋值
  //        TAX_RATE2 = 2.2;
  //    }
  
      static {//代码块中赋值
          TAX_RATE3 = 3.5;
      }
  }
  
  ```

- final 和 static 往往搭配使用，效率更高，不会导致类加载，底层编译器做了优化处理
### 流程控制 

#### 条件

- if......else

  ```java
  public class Test {
     public static void main(String args[]){
        int x = 10;
         
        if( x < 20 ){
           System.out.print("这是 if 语句");
        }
     }
  }
  
  ```
  
- if...else if...else 语句

  ```java
  public class Test {
     public static void main(String args[]){
        int x = 30;
         
        if( x == 10 ){
           System.out.print("Value of X is 10");
        }else if( x == 20 ){
           System.out.print("Value of X is 20");
        }else if( x == 30 ){
           System.out.print("Value of X is 30");
        }else{
           System.out.print("这是 else 语句");
        }
     }
  }
  
  ```
  
- 嵌套的if...else语句

  ```java
  public class Test {
     public static void main(String args[]){
        int x = 30;
        int y = 10;
         
        if( x == 30 ){
           if( y == 10 ){
               System.out.print("X = 30 and Y = 10");
            }
         }
      }
  }
  
  ```

#### 循环

- while() 语句

  ```java
  public class Test {
     public static void main(String args[]) {
        int x = 10;
         
        while( x < 20 ) {
           System.out.print("value of x : " + x );
           x++;
           System.out.print("\n");
        }
     }
  }
  
  ```
  
- do...while(); 语句

  ```java
  public class Test {
     public static void main(String args[]){
        int x = 10;
   
        do{
           System.out.print("value of x : " + x );
           x++;
           System.out.print("\n");
        }while( x < 20 );
     }
  }
  
  ```
  
- for 语句

  ```java
  public class Test {
     public static void main(String args[]) {
     
        for(int x = 10; x < 20; x = x+1) {
           System.out.print("value of x : " + x );
           System.out.print("\n");
        }
     }
  }
  
  ```

- foreach 语句 （for语句的增强）

  ```java
  public class Test {
      /*
          for(声明语句 : 表达式)
          {
             //代码句子
          }
      */
     public static void main(String args[]){
        int [] numbers = {10, 20, 30, 40, 50};
   
        for(int x : numbers ){
           System.out.print( x );
           System.out.print(",");
        }
        System.out.print("\n");
        String [] names ={"James", "Larry", "Tom", "Lacy"};
        for( String name : names ) {
           System.out.print( name );
           System.out.print(",");
        }
     }
  }
  
  ```
  
- switch...case

  ```java
  public class Test {
     public static void main(String args[]){
        //char grade = args[0].charAt(0);
        char grade = 'C';
   
        switch(grade)
        {
           case 'A' :
              System.out.println("优秀"); 
              break;
           case 'B' :
           case 'C' :
              System.out.println("良好");
              break;
           case 'D' :
              System.out.println("及格");
              break;
           case 'F' :
              System.out.println("你需要再努力努力");
              break;
           default :
              System.out.println("未知等级");
        }
        System.out.println("你的等级是 " + grade);
     }
  }
  
  ```

## 数组

- 数组的创建

  ```java
  //方法1
  dataType[] arrayRefVar = new dataType[arraySize];
  //方法2
  dataType[] arrayRefVar = {value0, value1, ..., valuek};
  
  ```

- 执行的步骤：

  ```
  1.使用 dataType[arraySize] 创建了一个数组
  2.把新创建的数组的引用赋值给变量 arrayRefVar
  
  ```

- 数组作为函数的参数

  ```java
  public static void main(String[] args) {
          printArray(new int[]{3, 1, 2, 6, 4, 2});
      /*
      或者分布操作
          int[] a = new int[]{3, 1, 2, 6, 4, 2};
          printArray(a);
      */
      }
      
  public static void printArray(int[] array) {
    for (int i = 0; i < array.length; i++) {
      System.out.print(array[i]+" ");
    }
  }
  
  ```

- 数组作为函数的返回值

  ```java
  /*
      可以实现数组中元素值的逆序
  */
  
  public static void main(String[] args) {
  
          int[] a = reverse(new int[]{1,2,3,4,5});
          for (int i=0; i<a.length; i++) {
              System.out.println(a[i]);
          }
      }
  
      public static int[] reverse(int[] list) {
          int[] result = new int[list.length];
          for (int i=0, j=result.length-1; i<list.length; i++, j--) {
              result[j] = list[i];
          }
          return result;
      }
  ```



## 对象和类（重点）

### 方法（等价与c/c++中的函数）

- 方法的说明![方法.jpg](https://i.loli.net/2021/11/04/lOLGbSyUVTs9B4M.jpg)

- 方法实例

  ```java
  /*  返回两个整型变量数据的较大值  */
  public static int max(int num1, int num2) {
     int result;
     if (num1 > num2)
        result = num1;
     else
        result = num2;
   
     return result; 
  }
  ```

- 方法的调用实例

  ```java
  public class TestMax {
     /** 主方法 main函数的入口  */  
     public static void main(String[] args) {
        int i = 5;
        int j = 2;
        int k = max(i, j);
        System.out.println( i + " 和 " + j + " 比较，最大值是：" + k);
     }
   
     /** 返回两个整数变量较大的值 */
     public static int max(int num1, int num2) {
        int result;
        if (num1 > num2)
           result = num1;
        else
           result = num2;
   
        return result; 
     }
  }
  ```

  

### 重写和重载

- 方法的重写（override）

  - 参数列表与被重写方法的参数列表必须完全相同。
  - 返回类型与被重写方法的返回类型可以不相同，但是必须是父类返回值的派生类（java5 及更早版本返回类型要一样，java7 及更高版本可以不同）。
  - 访问权限不能比父类中被重写的方法的访问权限更低。例如：如果父类的一个方法被声明为 public，那么在子类中重写该方法就不能声明为 protected。
  - 父类的成员方法只能被它的子类重写。
  - 声明为 final 的方法不能被重写。
  - 声明为 static 的方法不能被重写，但是能够被再次声明。
  - 子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为 private 和 final 的方法。
  - 子类和父类不在同一个包中，那么子类只能够重写父类的声明为 public 和 protected 的非 final 方法。
  - 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。

- 重载（overload）

  - 重载是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。

  - 每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。

  - 最常用的地方就是构造器的重载。

- 总结 (重写和重载的比较)

  - 图例![img](https://www.runoob.com/wp-content/uploads/2013/12/overloading-vs-overriding.png)
  
  - 比较
  
    |       名称       | 发生范围 |  方法名  |             参数列表             |                           返回类型                           |               修饰符               |
    | :--------------: | :------: | :------: | :------------------------------: | :----------------------------------------------------------: | :--------------------------------: |
    | 重载（overload） |   本类   | 必须一样 | 类型，个数或者顺序至少有一个不同 |                            无要求                            |               无要求               |
    | 重写（override） | 父 子类  | 必须一样 |               相同               | 子类重写的方法，返回的类型和父类返回的类型一致，或者是其子类 | 子类方法不能缩小父类方法的访问范围 |
  
  

### 封装

- 封装干什么用？
  
  - 可以使本类中private属性的成员变量或方法可以被类外访问。
  - 使得要访问该类的代码和数据就必须通过接口控制。
  
- 实例  (get/set)

  ```java
  /* 文件名: EncapTest.java */
  public class EncapTest{
   /*
   	这段代码中，将 name、idNum 和 age 属性设置为私有的，只能本类才能访问，其他类都访问不了，如此就对信息进行了隐藏。
   */
     private String name;
     private String idNum;
     private int age;
   
  /*
  	对每个值属性提供对外的公共方法访问，也就是创建一对赋取值方法，用于对私有属性的访问，例如：
  */
     public int getAge(){
        return age;
     }
      
     public String getName(){
        return name;
     }
   
     public String getIdNum(){
        return idNum;
     }
   
     public void setAge( int newAge){
        age = newAge;
     }
   
     public void setName(String newName){
        name = newName;
     }
   
     public void setIdNum( String newId){
        idNum = newId;
     }
  }
  ```

  

### 继承

- extends 关键字

  ```java
  package com.pyextend;
  
  /* 	在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。继承只能实现单继承 A--->B--->C   B--->D
  */
  
  public class Animal {
      private String name;
      private int id;
      //私有属性进行封装
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
      
      public int getId() {
          return id;
      }
      
      public void setId(int id) {
          this.id = id;
      }
  
      //父类的构造器 有参构造器
      public Animal(String myname, int myid) {
          //初始化属性值
          this.name = myname;
          this.id = myid;
      }
  
      public void eat() {
          //吃东西方法的具体实现
      }
  
      public void sleep() {
          //睡觉方法的具体实现
      }
  }
  
  class Penguin extends Animal {
  
      private String color;
      //私有属性进行封装
      public String getColor() {
          return color;
      }
  
      public void setColor(String color) {
          this.color = color;
      }
      //子类的有参构造器
      public Penguin(String myname, int myid, String color) {
          //父类的构造器完成父类的初始化
          //子类的构造器完成子类的初始化
          super(myname, myid); //使用super关键字调用父类的初始化
          this.color = color;
      }
  }
          
  ```

- implements 关键字

  ```java
  /*	使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。*/
  public interface A {  //接口A
      public void eat();
      public void sleep();
  }
   
  public interface B { //接口B
      public void show();
  }
   
  public class C implements A,B {   //C继承接口A、B
  }
  
  
  /*接口的继承实例*/
  /* 注意事项：
          1.一个类可以同时实现多个接口。
          2.一个类只能继承一个类，但是能实现多个接口。
          3.一个接口能继承另一个接口，这和类之间的继承比较相似。
  */
  // 文件名: Sports.java
  public interface Sports
  {
     public void setHomeTeam(String name);
     public void setVisitingTeam(String name);
  }
   
  // 文件名: Football.java
  public interface Football extends Sports
  {
     public void homeTeamScored(int points);
     public void visitingTeamScored(int points);
     public void endOfQuarter(int quarter);
  }
   
  // 文件名: Hockey.java
  public interface Hockey extends Sports
  {
     public void homeGoalScored();
     public void visitingGoalScored();
     public void endOfPeriod(int period);
     public void overtimePeriod(int ot);
  }
  ```

- super和this 关键字

  | No.  | 区别点     | this                                                     | super                                    |
  | ---- | ---------- | -------------------------------------------------------- | ---------------------------------------- |
  | 1    | 访问属性   | 访问本类中的属性，如果本类没有此属性，则从父类中继续查找 | 从父类开始查找属性                       |
  | 2    | 调用方法   | 访问本类中的方法，如果本类中没有此方法则从父类继续查找   | 从父类开始查找方法                       |
  | 3    | 调用构造器 | 调用本类构造器，必须放在构造器的首行                     | 调用父类构造器，必须放在子类构造器的首行 |
  | 4    | 特殊       | 表示当前对象                                             | 子类中访问父类对象                       |

  ```java
  //父类和子类都有一个方法call()
  /*  需要注意的是找call()和this.call()，的顺序是：
  	(1)先找本类，如果有，则调用
  	(2)如果没有，则找父类（如果有，并可以调用，则调用）
  	(3)如果父类没有，则继续找父类的父类，整个规则，就是一样的，直到 Object 类
  	提示：如果查找方法的过程中，找到了，但是不能访问，则报错，cannot access
  	     如果查找方法的过程中，没有找到，则提示方法不存在
  	其中super.call()先查找父类，其他规则一样
  */
  
  /*
  	super关键字：我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类。
  	super的访问不限于直接父类，如果爷爷类和本类中有同名的成员，也可以使用super去访问爷爷类的成员;如果多个基类(上级类)中都有同名的成员，使用super访问遵循就近原则。A->B->C
  	this关键字：指向自己的引用。
  */
  
  //父类
  class Animal {
    void eat() {
      System.out.println("animal : eat");
    }
  }
  
  //子类
  class Dog extends Animal {
    void eat() {
      System.out.println("dog : eat");
    }
      
    void eatTest() {
      this.eat();   // this 调用自己的方法
      super.eat();  // super 调用父类方法
    }
  }
   
  public class Test {
    public static void main(String[] args) {
      Animal a = new Animal();
      a.eat();
      Dog d = new Dog();
      d.eatTest();
    }
  }
  ```

- final 关键字

  ```java
  /*	final 关键字声明类可以把类定义为不能继承的，即最终类；或者用于修饰方法，该方法不能被子类重写：*/
  
  //声明类:
  final class 类名 {//类体}
  
  //声明方法:
  修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}
      
  ```

  

### 多态

- 多态存在的三个必要条件
  - 继承
  - 重写
  - 父类引用指向子类对象：**Parent p = new Child();**

- 多态的具体体现形式

  - 第一种：方法的对象    即重载、重写就体现多态

  - 第二种：对象的多态（**核心、难点、重点**）

    ✳**老韩总结的几句重要的话（记住）：**

    （1）一个对象的编译类型和运行类型可以不一致

    （2）编译类型在定义对象时，就确定了，不能改变

    （3）运行类型是可以变化的

    （4）**编译类型**看定义时  =  号 的左边，**运行类型**  = 号 的右边 

    - 解释说明

      ```java
      /*（Animal animal ------> 父类的引用）
        （new Dog() -----> 子类的对象）       */
      Animal animal = new Dog();  //【animal 编译类型是Animal，运行类型为Dog】
      animal = new Cat(); //【animal 的运行类型变成了 Cat，编译类型仍然是 Animal】
      ```
    
    - 父类的引用指向子类的对象（向上转型）
    
      ```java
      public static void main(String[] args) {
              //父类的引用指向子类的对象（向上转型）
              Animal animal= new Cat();
              //Object obj = new Cat(); //可以吗？可以 Object 也是 Cat 的父类
              /*向上转型调用方法的规则如下：
                  (1)可以调用父类中的所有成员（需遵守访问权限）
                  (2)不能调用子类的特有成员
                  (3)因为在编译阶段，能调用哪些成员，是由编译类型来决定的
                  animal.catchMouse();错误
                  (4)最终运行效果看子类（运行类型）的具体实现，即调用方法时，按照从子类（运行类型），开始查找方法，然后调用，规则和前面的调用规则一致   */
              animal.eat();//猫吃鱼   (子类中的是猫吃鱼，父类中是吃)
              animal.sleep();//睡
              animal.run();//跑
              animal.show();//hello,你好
          }
      ```
    
    - 向下转型
    
      ```java
      public static void main(String[] args) {
             
             //~~~~~~~减少篇幅 省略上面向上转型的代码 
             //下面的代码 接上面的代码
             
              //假如说，想要调用Cat 的 catchMouse 方法
              //多态的向下转型
              //(1)语法：子类类型 引用名 = （子类类型）父类引用
              // Cat编译类型是 Cat   运行类型也是 Cat
              Cat cat = (Cat) animal;
              cat.catchMouse();//猫抓老鼠
              //(2)要求父类的引用必须指向的是当前目标类型的对象
          }
      ```
    
    - 属性没有重写之说！**属性的值看编译类型**
    
      ```java
      public class Animal {
          public static void main(String[] args) {
              Base base = new Base();
              System.out.println(base.count);//看编译类型 Base 结果 10
      
              Sub sub = new Sub();
              System.out.println(sub.count);//编译类型 Sub 结果 20
          }
      }
      
      class Base{
          int count = 10;
      }
      class Sub extends Base{
          int count = 20;
      }
      ```
    
    - instanceof 比较操作符，用于判断**对象的运行类型**是否为XX类型或者XX类型的子类型
    
      ```java
      public class Animal {
          public static void main(String[] args) {
              BB b = new BB();
              System.out.println(b instanceof AA);//true
              System.out.println(b instanceof BB);//true
              
              //编译类型 AA  运行类型 BB
              AA a = new BB();
              System.out.println(a instanceof AA);//true
              System.out.println(a instanceof BB);//true
          }
      }
      
      class AA{ } //父类
      class BB extends AA{ } //子类
      ```

- （★）多态的动态绑定机制

  ```java
  public class Animal {
      public static void main(String[] args) {
          AA a = new BB();
          System.out.println(a.sum());//40 -->30
          System.out.println(a.sum1());//30 -->20
      }
  }
  
  class AA{ //父类
      public int i = 10;
      public int getI(){
          return i;
      }
      public int sum(){
          return getI() + 10; //getI() 看运行类型BB 所以还是要找子类中的getI() 所以结果阶变成了 20 + 10 == 30
      }
      public int sum1(){
          return  i + 10;   //同理子类找不到sum1()，所以到父类中找，找到了，返回 10 + 10 == 20 
      }
  }
  
  class BB extends AA{ //子类
      public int i = 20;
  //    public int sum() {
  //        return i + 20;
  //    }
      public int getI() {
          return i;
      }
  //    public int sum1() {
  //        return i + 10;
  //    }
  }
  ```

- 多态的实例

  ```java
  public class Test {
      public static void main(String[] args) {
        show(new Cat());  // 以 Cat 对象调用 show 方法
        show(new Dog());  // 以 Dog 对象调用 show 方法
                  
        Animal a = new Cat();  // 向上转型  
        a.eat();               // 调用的是 Cat 的 eat
        Cat c = (Cat)a;        // 向下转型  
        c.work();        // 调用的是 Cat 的 work
    }  
              
     public static void show(Animal a)  {
        a.eat();  
          // 类型判断
          if (a instanceof Cat)  {  //猫做的事情 
              Cat c = (Cat)a;  
              c.work();  
          } else if (a instanceof Dog) { //狗做的事情 
              Dog c = (Dog)a;  
              c.work();  
          }  
      }  
  }
   
  abstract class Animal {  
      abstract void eat();  
  }  
    
  class Cat extends Animal {  
      public void eat() {  
          System.out.println("吃鱼");  
      }  
      public void work() {  
          System.out.println("抓老鼠");  
      }  
  }  
    
  class Dog extends Animal {  
      public void eat() {  
          System.out.println("吃骨头");  
      }  
      public void work() {  
          System.out.println("看家");  
      }  
  }
  
  
  /* 运行结果：
  吃鱼
  抓老鼠
  吃骨头
  看家
  吃鱼
  抓老鼠
  */
  ```



## Object类详解

- equals方法【判断字符串类型是否相等】

  - == 和 equals的对比

    ```
    == 是一个比较运算符
    1. == : 既可以判断基本类型，又可以判断引用类型
    2. == : 如果判断基本类型，判断的是值是否相等，示例：int i=10；double d = 10.0
    3. == : 如果判断引用类型，判断的是地址是否相等，即判定是不是同一对象
    4.equals: 是Object类中的方法，只能判断引用类型
    默认判断的是地址是否相等，子类中往往重写该方法，用于判断内容是否相等。
    ```

- toString方法【返回字符串】
- finalize方法【垃圾回收（销毁）释放内存】



## 断点调试（debug）

在IDEA中会设置断点，使用debug进行调试。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   



## 类变量和类方法

（1）类方法和普通方法都是随着类的加载，将结构信息存储在方法区：

​		类方法中无this的参数

​		普通方法中隐含着this的参数

（2）类方法可以通过类名调用，也可以通过对象名调用

（3）普通方法和对象有关，需要通过对象名调用

（4）类方法中不允许使用和对象有关的关键字，比如this和super。普通方法（成员方法）可以。

（5）类方法（静态方法）中 只能访问 静态变量 或静态方法。

（6）普通成员方法，既可以访问 非静态成员，也可以访问静态成员。

- **小结**：**静态方法，只能访问静态的成员，非静态的方法，可以访问静态成员和非静态成员**。



## main函数和代码块

- 对main函数的理解   public static void main(String[] args) 

- 对使用代码块

  ```
  如果类有多个构造器，那么就可以将这些构造器中共有的代码放到一个代码块中
  (1)这样我们就可以把相同的语句，放入到一个代码块中
  (2)这样当我们不管调用哪个构造器，创建对象，都会先调用代码块中的内容
  (3)代码块调用的顺序优先于构造器
  ```

- 代码块的使用细节

  ```
  1、static代码块也叫静态代码块，作用就是对类进行初始化，而随着类的加载而执行，并且只会执行一次。如果是普通代码块，每创建一个对象，就执行。
  
  2、类什么时候被加载【重要】
  	(1)创建对象实例时(new)
  	(2)创建子类对象实例，父类也会被加载 (父类先被加载，子类后被加载)
  	(3)使用类的静态成员时(静态属性，静态方法)
  	
  3、普通的代码块，在创建对象实例时，会被隐式的调用。
  	被创建一次，就会被调用一次
  	如果只是使用类的静态成员时，普通代码块并不会执行
  	
  4、创建一个对象时，在一个类 调用顺序是:【重点、难点】
  	(1)调用静态代码块和静态属性初始化 (注意:静态代码块和静态属性初始化调用的优先级一样，如果有多个静态代码块和多个静态变量初始化，则按照他们定义的顺序调用)
  	(2)调用普通代码块和普通属性的初始化(注意: 普通代码块和普通属性初始化调用的优先级一样，如果有多个普通代码块和多个普通属性初始化，则按照定义顺序调用)
  	(3)调用构造方法。
  
  5、构造器 的最前面其实隐含了 super()和调用普通代码块，静态相关的代码块，属性的初始化，在类加载时，就执行完毕，因此是由优先于 构造器和普通代码块执行的
  
  6、我们看一下创建一个子类对象时(继承关系)，他们的静态代码块，静态属性初始化，普通代码块，普通属性初始化，构造方法的调用顺序如下：//面试题
      (1)父类的静态代码块和静态属性(优先级一样，按定义顺序执行)
      (2)子类的静态代码块和静态属性(优先级一样，按定义顺序执行)
      (3)父类的普通代码块和普通属性初始化(优先级一样，按定义顺序执行)
      (4)父类的构造方法
      (5)子类的普通代码块和普通属性初始化(优先级一样，按定义顺序执行)
      (6)子类的构造方法
  	分析:(1)进行类的加载【加载时先执行静态的东西，顺序：父类-->子类】
  	(2)创建对象【开始执行构造器(里面默认隐藏了super，所以执行顺序：super()-->普通的东西--> 构造器里面的东西)】
  
  7、静态代码块只能直接调用静态成员(静态属性和静态方法)，普通代码块可以调用任意成员
  ```



## 单例模式

- 什么是单例设计模式？

- 单例（即：单个实例）

  1、所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类只能存在以一个对象实例，并且该类只提供一个取得其对象实例的方法

  2、单例模式有两种方式： 饿汉式和懒汉式

- 步骤如下：

  （1）构造器私有化

  （2）类的内部创建对象

  （3）向外暴露一个静态的公共方法

  （4）代码实现

### 单例模式【饿汉式】

```java
package com.designpattern;

public class DesignPattern01 {
    public static void main(String[] args) {
        /*GirlFriend gf1 = new GirlFriend("小红");
        GirlFriend gf2 = new GirlFriend("小白");
        System.out.println(gf1);
        System.out.println(gf2);*/
		
        //这样就保证了一个类只有一个对象，不能再外部new多个对象了
        System.out.println(GirlFriend.getInstance()); 
        
    }
}

//有一个类，GirlFiend
//只能有一个女朋友

class GirlFriend{
    private String name;

    //如何保证我们只能创建一个 GirlFriend 对象
    //步骤【单例模式-饿汉式】(饿汉式：在类被加载时就已经创建好了)
    //1 将构造器私有化
    //2 在类的内部直接创建一个对象(该对象时static)
    //3 提供一个公共的 static 方法，返回 gf 对象
    private static GirlFriend gf = new GirlFriend("小红");

    private GirlFriend(String name) {
        this.name = name;
    }

    public static GirlFriend getInstance(){
        return gf;
    }
    
    @Override
    public String toString() {
        return "GirlFriend{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

### 单例模式【懒汉式】

```java
package com.designpattern;

/**
 * 演示懒汉式
 */
public class DesignPattern02 {
    public static void main(String[] args) {

        System.out.println(Cat.getInstance());
    }
}

//希望在程序运行过程中，只创建一个Cat 对象
//使用单例模式

class Cat{
    private String name;

    //步骤
    //1 仍然将构造器私有化
    //2 定义一个static 静态属性对象
    //3 提供一个public 的static 方法，可以返回一个Cat 对象
    //4 懒汉式，只有当用户使用getInstance时，才返回cat对象，当再次调用时则会返回上一次创建的cat对象
    //从而保证了单例
    private static Cat cat;

    private Cat(String name) {
        this.name = name;
    }

    public static Cat getInstance(){
        if (cat == null){ //如果还没有创建cat对象
            cat = new Cat("金毛");
        }
        return cat;
    }

    @Override
    public String toString() {
        return "Cat{" +
                "name='" + name + '\'' +
                '}';
    }
}
```



## 抽象类

- 抽象类的总结规定

  ```
  1. 抽象类不能被实例化(初学者很容易犯的错)，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。
  2. 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
  3. 抽象类中的抽象方法只是声明，不包含方法体，就是不给出方法的具体实现，也就是方法的具体功能。
  4. 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。
  5. 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。
  ```

- 使用 abstract class 定义抽象 Employee 类

  ```java
  /* 文件名 : Employee.java */
  public abstract class Employee
  {
     private String name;
     private String address;
     private int number;
      
    public Employee(String name, String address, int number)//初始化构造函数
    {
       System.out.println("Constructing an Employee");
       this.name = name;
       this.address = address;
       this.number = number;
    }
      
    public double computePay()
    {
      System.out.println("Inside Employee computePay");
      return 0.0;
    }
    public void mailCheck()
    {
       System.out.println("Mailing a check to " + this.name
        + " " + this.address);
    }
     //c
    public String toString()
    {
       return name + " " + address + " " + number;
    }
    public String getName()
    {
       return name;
    }
    public String getAddress()
    {
       return address;
    }
    public void setAddress(String newAddress)
    {
       address = newAddress;
    }
    public int getNumber()
    {
      return number;
    }
  }
  ```
  
- 继承抽象 Employee 类的 Salary 子类

  ```java
  /* 文件名 : Salary.java */
  public class Salary extends Employee
  {
     private double salary; //Annual salary
     public Salary(String name, String address, int number, double
        salary)
     {
         super(name, address, number);
         setSalary(salary);
     }
     public void mailCheck()
     {
         System.out.println("Within mailCheck of Salary class ");
         System.out.println("Mailing check to " + getName()
         + " with salary " + salary);
     }
     public double getSalary()
     {
         return salary;
     }
     public void setSalary(double newSalary)
     {
         if(newSalary >= 0.0)
         {
            salary = newSalary;
         }
     }
     public double computePay()
     {
        System.out.println("Computing salary pay for " + getName());
        return salary/52;
     }
  }
  
  /*
  尽管我们不能实例化一个 Employee 类的对象，但是如果我们实例化一个 Salary 类对象，该对象将从 Employee 类继承 7 个成员方法，且通过该方法可以设置或获取三个成员变量。
  */
  
  /* 文件名 : AbstractDemo.java (main 入口） */
  public class AbstractDemo
  {
     public static void main(String [] args)
     {
        Salary s = new Salary("Mohd Mohtashim", "Ambehta, UP", 3, 3600.00);
        Employee e = new Salary("John Adams", "Boston, MA", 2, 2400.00);
   
        System.out.println("Call mailCheck using Salary reference --");
        s.mailCheck();
   
        System.out.println("\n Call mailCheck using Employee reference--");
        e.mailCheck();
      }
  }
  
  ```

- 抽象方法的实例

  ```java
  public abstract class Employee
  {
     private String name;
     private String address;
     private int number;
     
     public abstract double computePay();
      
     //其余代码
  }
  ```




## 接口

- 接口的特性

  ```
  1. 接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 public abstract（只能是 public abstract，其他修饰符都会报错）。
  2.接口中可以含有变量，但是接口中的变量会被隐式的指定为 public static final 变量（并且只能是 public，用 private 修饰会报编译错误）。
  3.接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。
      
  小结：
      1.在jdk7.0前 接口里的所有方法都没有方法体，即都是抽象方法
      2.Jdk8.0后 接口可以有静态方法，默认方法，也可以有方法的具体实现。
      
  ```

- 接口特性的实例

  ```java
  /*  1.接口是隐式抽象的，当声明一个接口的时候，不必使用abstract关键字。
     	2.接口中每一个方法也是隐式抽象的，声明时同样不需要abstract关键字。
      3.接口中的方法都是公有的。   */
  
  /* 文件名 : Animal.java */
  interface Animal {
     public void eat();
     public void travel();
  }
  
  ```

- ✳抽象类和接口的区别

  ```java
  1. 抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
  2. 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 public static final 类型的。
  3. 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
  4. 一个类只能继承一个抽象类，而一个类却可以实现多个接口。
      
  ```

- 接口的声明

  ```java
  //语法格式：
  [可见度] interface 接口名称 [extends 其他的接口名] {
          // 声明变量
          // 抽象方法
  }
  
  //声明接口的例子:
  /* 文件名 : NameOfInterface.java */
  import java.lang.*;  //引入包
  
  public interface NameOfInterface
  {
     //任何类型 final, static 字段
     //抽象方法
  }
  
  ```

- 接口的实现

  ```java
  /*	注意：当类实现接口的时候，类要实现接口中所有的方法。否则，类必须声明为抽象的类。
  	类使用implements关键字实现接口。在类声明中，Implements关键字放在class声明后面。 */
  
  /* 文件名 : MammalInt.java */  
  public class MammalInt implements Animal{
   
     public void eat(){
        System.out.println("Mammal eats");
     }
   
     public void travel(){
        System.out.println("Mammal travels");
     } 
   
     public int noOfLegs(){
        return 0;
     }
   
     public static void main(String args[]){
        MammalInt m = new MammalInt();
        m.eat();
        m.travel();
     }
  }
  
  /*运行结果：
  Mammal eats
  Mammal travels
  */
  
  ```

- 接口的继承 （见对象和类中）

- 多继承和标记接口

  - 接口的多继承

    ```java
    /*	在Java中，类的多继承是不合法，但接口允许多继承。在接口的多继承中extends关键字只需要使用一次，在其后跟着继承接口。*/
    public interface Hockey extends Sports, Event
        
    ```

  - 标记接口

    ```java
    /*	最常用的继承接口是没有包含任何方法的接口。
    
    标记接口是没有任何方法和属性的接口.它仅仅表明它的类属于一个特定的类型,供其他代码来测试允许做一些事情。
    
    标记接口作用：简单形象的说就是给某个对象打个标（盖个戳），使对象拥有某个或某些特权。
    
    例如：java.awt.event 包中的 MouseListener 接口继承的 java.util.EventListener 接口定义如下：	*/
    
    package java.util;
    public interface EventListener
    { 	}
    
    ```

- 接口 VS 继承

  ```
  小结：
      当子类继承了父类，就自动的拥有了父类的而功能
      如果子类需要扩展功能，就可以通过实现接口的方式扩展
      可以理解 实现接口 是对 java 单继承机制的一种补充
  ```



## 类的五大成员

- 属性
- 方法
- 构造器
- 代码块
- 内部类

### 内部类详解

- 什么是内部类?

  ```
  一个类的内部又完整的嵌套了另一个类结构。被嵌套的类称为内部类(inner class),嵌套其他类的类称为外部类(outer class)
  ```

- 基本语法

  ```java
  class Outer{   //外部类
  	class Inner{   //内部类
  	}
  }
  class Other{ //外部其他类
  }
  ```

- 内部类的分类

  - 定义在外部类局部位置上（比如说方法体）
  
    （1）局部内部类（有类名）
  
    ```
    局部内部类是定义在外部类的局部位置，比如方法中，并且有类名
    1.可以直接访问外部类的所有成员，包括私有的
    2.不能添加访问修饰符，因为它的地位就是一个局部变量。局部变量是不能使用修饰符的。但是可以使用final 修饰，因为局部变量也可以使用final
    3.作用域：仅仅在定义它的方法或者代码块中。
    4.局部内部类---访问--->外部类的成员【访问方式：直接访问】
    5.外部类---访问--->局部内部类的成员
    	访问方式：创建对象，再访问【即在外部类方法中new 内部类的对象 然后访问】(注意：必须在作用域内)
    6.外部其他类---不能访问--->局部内部类(因为 局部内部类的地位是一个局部变量)
    7.如果外部类和局部内部类的成员重名时，默认遵循就近原则，如果想访问外部类的成员
    则可以使用 (外部类名.this.成员) 去访问
    	
    ```
  
    （2）匿名内部类（没有类名）
  
    ```
    匿名内部类的使用：
    (1)本质是类(2)内部类(3)该类没有名字(4)同时还是一个对象
    说明：匿名内部类是定义在外部类的局部位置，比如方法中，并且没有类名
    1.匿名内部类的基本语法
    new 类或接口(参数列表){
    	类体
    };
    ```
  
    - 基于接口的使用实例
  
      ```java
      package com.inner_class.Anonymous;
      
      public class AnonymousInnerClass {
          public static void main(String[] args) {
              Others others = new Others();
              others.method();
          }
      }
      
      class Others { //外部类
          private int n1 = 10;
          public void method() { //方法
      //        IA tiger = new Tiger();
      //        tiger.cry();
      //        IA dog = new Dog();
      //        dog.cry();
              //1.需求：想使用IA接口，并创建对象
              //2.传统方法，是写一个类，实现该接口，并创建对象
              //3.实际需求是 Tiger/Dog 类只是使用一次，后面在不使用
              //4.可以使用匿名内部类来简化开发
              //5.tiger 的编译类型 ？ ====> IA
              //6.tiger 运行类型  ？ =====>   Others$1
              /* 
              匿名内部类的类名系统自动分配，这里可以使用 对象.getClass() 来查看一下
              class Others$1 implements IA{
                  @Override
                  public void cry() {
                      System.out.println("老虎在交换...");
                  }
              }
              */
              //7.jdk 底层在创建匿名内部类 Others$1 时，立刻马上就创建了 Others$1 实例,并且把地址返回给 tiger
              IA tiger = new IA() {
                  @Override
                  public void cry() {
                      System.out.println("老虎在叫唤...");
                  }
              };
              tiger.cry();
              System.out.println("Outer 的运行内存 " + tiger.getClass());
      
          }
      }
      
      interface IA { //接口
          void cry();
      }
      
      //class Tiger implements IA{
      //    @Override
      //    public void cry() {
      //        System.out.println("老虎在叫唤.....");
      //    }
      //}
      
      //class Dog implements IA{
      //    @Override
      //    public void cry() {
      //        System.out.println("小狗在叫唤.....");
      //    }
      //}
      
      ```
  
    - 基于接口的使用实例
  
      ```java
      package com.inner_class.Anonymous;
      
      public class AnonymousInnerClass {
          public static void main(String[] args) {
              Others others = new Others();
              others.method();
          }
      }
      
      class Others { //外部类
          private int n1 = 10;
      
          public void method() { //方法
              //分析：
              //1.father 编译类型 Father
              //2.father 运行类型 Others$1
              //3.底层会创建匿名内部类
              /*
              底层实现的的东西 类名 仍然是系统分配的类名
              class Others$1 extends Father{
                  public Others$1(String name) {
                      super(name);
                  }
                  @Override
                  public void test() {
                      System.out.println("匿名内部类重写了test方法....");
                  }
              }
               */
              Father father = new Father("jack") {
                  @Override
                  public void test() {
                      System.out.println("匿名内部类重写了test方法....");
                  }
              };
              father.test();
              System.out.println("匿名内部类的 " + father.getClass());
          }
      }
      
      class Father { //类
          public Father(String name) {
          }//构造器 
      
          public void test() {
          }
      }
      
      ```
      
      ```java
      //匿名内部类的实例
      package com.inner_class.Anonymous;
      
      public class AnonymousInnerClass {
          public static void main(String[] args) {
              CellPhone cellPhone = new CellPhone();
              cellPhone.alarmClock(new Bell() {
                  @Override
                  public void ring() {
                      System.out.println("懒猪起床了....");
                  }
              });
              cellPhone.alarmClock(new Bell() {
                  @Override
                  public void ring() {
                      System.out.println("小伙伴上课了.....");
                  }
              });
          }
      }
      
      interface Bell{
          void ring();
      }
      
      class CellPhone{
          public void alarmClock(Bell bell){
              bell.ring();
          }
      }
      
      ```
      
  
  - 定义在外部类的成员位置上：
  
    （1）成员内部类（没用static修饰）
  
    ```
    说明:成员内部类是定义在外部类的成员位置，并且没有static修饰
    1.可以直接访问外部类的所有成员，包括私有的
    2.可以添加任意成员访问修饰符(public、protected、默认、private),因为它就是一个成员
    3.作用域和访问自己试一下即可(不难)
    ```
    
    （2）静态内部类（使用static修饰）
    
    ```
    说明:静态内部类是定义在外部类的成员位置，并且有static修饰
    1.可以直接访问外部类的所有静态成员，包括私有的，但是不能直接访问非静态成员
    2.可以添加任意成员访问修饰符(public、protected、默认、private),因为它就是一个成员
    3.作用域：同其他的成员，为整个整体
    ```
    
    

## 枚举

- 枚举类的注意事项

  ```
  使用enum关键字后，就不能再继承其他类了，因为enum会隐式继承Enum，而Java是单继承机制
  枚举类和普通类一样，可以实现接口，如下形式：
  enum 类名 implements 接口1,接口2{}
  ```

- 枚举实例

  ```java
  enum Color     //枚举的关键字enum，常量用“,”隔开
  {
      RED, GREEN, BLUE;
  }
   
  public class Test
  {
      // 执行输出结果
      public static void main(String[] args)
      {
          Color c1 = Color.RED;
          System.out.println(c1);
      }
  }
  ```

- 内部类中使用枚举    (与类外的效果一致)

  ```java
  public class Test  //Test类
  {
      enum Color
      {
          RED, GREEN, BLUE;
      }
   
      // 执行输出结果
      public static void main(String[] args)
      {
          Color c1 = Color.RED;
          System.out.println(c1);
      }
  }
  
  /*每个枚举都是通过 Class 在内部实现的，且所有的枚举值都是 public static final 的。 */
   
  /*		以上的枚举类 Color 转化在内部类实现： 
      class Color
      {
           public static final Color RED = new Color();
           public static final Color BLUE = new Color();
           public static final Color GREEN = new Color();
      }
  */
  ```

- 外部枚举类中抽象方法的实现

  ```java
  enum Color{
      RED{
          public String getColor(){//枚举对象实现抽象方法
              return "红色";
          }
      },
      GREEN{
          public String getColor(){//枚举对象实现抽象方法
              return "绿色";
          }
      },
      BLUE{
          public String getColor(){//枚举对象实现抽象方法
              return "蓝色";
          }
      };
      public abstract String getColor();//定义抽象方法
  }
  
  public class Test{
      public static void main(String[] args) {
          for (Color c:Color.values()){
              System.out.print(c.getColor() + " ");
          }
      }
  }
  ```

- 枚举的迭代 （for语句、switch 语句）

  -  for 语句迭代枚举元素

    ```java
    enum Color
    {
        RED, GREEN, BLUE;
    }
    
    public class MyClass {
      public static void main(String[] args) {
        for (Color myVar : Color.values()) {
          System.out.println(myVar);
        }
      }
    }
    /*输出结果：
    RED
    GREEN	
    BLUE
    */
    ```

  -  switch 语句枚举类的实现

    ```java
    enum Color
    {
        RED, GREEN, BLUE;
    }
    
    public class MyClass {
      public static void main(String[] args) {
        Color myVar = Color.BLUE;
    
        switch(myVar) {
          case RED:
            System.out.println("红色");
            break;
          case GREEN:
             System.out.println("绿色");
            break;
          case BLUE:
            System.out.println("蓝色");
            break;
        }
      }
    }
    /*输出结果：
    蓝色
    */
    ```
  
- 枚举类的父类Enum类中的一些方法 

  > 注：enum 定义的枚举类默认继承了 java.lang.Enum 类，并实现了 java.lang.Seriablizable 和 java.lang.Comparable 两个接口。values(), ordinal() 和 valueOf() 方法位于java.lang.Enum 类中。
  >

  - values()： 返回枚举类中所有的值。
  - ordinal()：方法可以找到每个枚举常量的索引，就像数组索引一样。
  - valueOf()：方法返回指定字符串值的枚举常量。

  ```java
  enum Color
  {
      RED, GREEN, BLUE;
  }
   
  public class Test
  {
      public static void main(String[] args)
      {
          // 调用 values()
          Color[] arr = Color.values();
   
          // 迭代枚举
          for (Color col : arr)
          {
              // 查看索引
              System.out.println(col + " at index " + col.ordinal());
          }
   
          // 使用 valueOf() 返回枚举常量，不存在的会报错 IllegalArgumentException
          System.out.println(Color.valueOf("RED"));
          // System.out.println(Color.valueOf("WHITE"));
      }
  }
  
  /*输出结果：
  RED at index 0
  GREEN at index 1
  BLUE at index 2
  RED
  */
  ```

- 枚举的类成员

  ```java
  enum Color
  {
      RED, GREEN, BLUE
   
      // 构造函数
      private Color()
      {
          System.out.println("Constructor called for : " + this.toString());
      }
   
      public void colorInfo()
      {
          System.out.println("Universal Color");
      }
  }
   
  public class Test
  {    
      // 输出
      public static void main(String[] args)
      {
          Color c1 = Color.RED;
          System.out.println(c1);
          c1.colorInfo();
      }
  }
  
  /*输出结果:
  Constructor called for : RED
  Constructor called for : GREEN
  Constructor called for : BLUE
  RED
  Universal Color
  */
  ```

- 枚举实例

  ```java
  package com.java_study.chapter11;
  
  public class Enumeration01 {
      public static void main(String[] args) {
          Week[] weeks = Week.values();
          System.out.println("========所有星期的信息如下=======");
          for (Week week:weeks) {
              System.out.println(week);
          }
      }
  }
  
  enum Week {
      MONDAY("星期一"),
      TUESDAY("星期二"),
      WEDNESDAY("星期三"),
      THURSDAY("星期四"),
      FRIDAY("星期五"),
      SATURDAY("星期六"),
      SUNDAY("星期日");
  
      private String name;
  
      Week(String name) {
          this.name = name;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      @Override
      public String toString() {
          return name;
      }
  
  }
  /*
  输出结果如下:
  ========所有星期的信息如下=======
  星期一
  星期二
  星期三
  星期四
  星期五
  星期六
  星期日
  */
  ```

  

## 常用类

### Integer 包装类

```java
package com.javaDemo.chapter12;

public class Integer01 {
    @SuppressWarnings({"all"})
    public static void main(String[] args) {
        //示例一
        Integer i1 = new Integer(127);
        Integer i2 = new Integer(127);
        System.out.println(i1 == i2);//F
        //示例二
        Integer i3 = new Integer(128);
        Integer i4 = new Integer(128);
        System.out.println(i3 == i4);//F
        //示例三
        Integer i5 = 127; //底层 Integer.ValueOf(127)
        Integer i6 = 127; //-128~127
        System.out.println(i5 == i6); //T
        //示例四
        Integer i7 = 128;
        Integer i8 = 128;
        System.out.println(i7 == i8); //F
        //示例五
        Integer i9 = 127;  //Integer.ValueOf(127)
        Integer i10 = new Integer(127);
        System.out.println(i9 == i10);  //F
        //示例六
        //只要有基本数据类型，判断的就是值是否相等
        Integer i11 = 127;
        int i12 = 127;
        System.out.println(i11 == i12); //T
        //示例七
        Integer i13 = 128;
        int i14 = 128;
        System.out.println(i13 ==i14);  //T
    }
}
```

### String 类

- 参考 String API   CSDN：https://blog.csdn.net/weixin_44141495/article/details/108100751


- 部分方法实例

  ```java
  public class Test01 {
      public static void main(String[] args) {
          String str = "我非常喜欢 1236";
          //str调用方法返回"1236"在str出现的位置
          int index = str.indexOf("1236");
          System.out.println(index);
          //str调用方法返回str中字符的个数
          int length = str.length();
          System.out.println(length);
          //str调用方法返回str中的字符：'喜'
          char c = str.charAt(3);
          System.out.println(c);
          //将字符串转换为字符数组
          char[] chars = str.toCharArray();
          //str调用方法返回字符串"1236"
          String temp = str.substring(6);
          String temp2 = str.substring(6, 8); // [6,8) 区间为左闭右开
          System.out.println(temp);
          System.out.println(temp2);
          //将temp转化为int型数据。
          int n = str.indexOf(temp);
          System.out.println(n);
      }
  }
  
  ```

- 字节/字符数组   转换成字符串

  ```
  byte[] bt = new byte[n];
  String s = new String(bt,0,n);
  
  char buf = new char[n]
  String str = new String(buf,0,n) //即从字符数组的下标0开始读取长度为n  转换为字符串
  ```

  ```
  b.inter()  方法返回常量池地址
  String s1 = "java"  【指向的是常量池】
  String s2 = new String("java") 【指向堆中的java】
  
  ```

- 字符串翻转例子

  ```java
  package com.javaDemo.date_.homework;
  
  public class HomeWork01 {
      public static void main(String[] args) {
          System.out.println(HomeWork01.reverse("abcdef",1,4));
      }
      
      public static String reverse(String str,int start,int end){
          char[] chars = str.toCharArray();
  
          for (int i = start,j = end; i < j; i++,j--) {
                  char temp = chars[i];
                  chars[i] = chars[j];
                  chars[j] = temp;
          }
          return new String(chars);
      }
  }
  
  ```

### StringBuffer 类

- StringBuffer 类的构造器

  ```
  StringBuffer类的构造器
  //1.创建一个 大小为 16的 char[] ,用于存放字符内容
  StringBuffer stringBuffer = new StringBuffer();
  //2.通过构造器指定 char[] 大小
  StringBuffer stringBuffer2 = new StringBuffer(20);
  //3.通过 给一个String 创建 StringBuffer
  StringBuffer hello = new StringBuffer("Hello")
  
  ```

- StringBuffer  和 String 相互转换

  ```
  //【String ----> StringBuffer】
  String str = "hello tom";
  //方式1 使用构造器
  StringBuffer stringBuffer = new StringBuffer(str);
  //方式2 使用append方法
  StringBuffer stringBuffer1 = new StringBuffer();
  stringBuffer1 = stringBuffer1.append(str);
  //【StringBuffer ----> String】
  StringBuffer stringBuffer3 = new StringBuffer("Hello ping");
  //方式1 使用StringBUffer 提供的 toString方法
  String s = stringBuffer3.toString();
  //方式2 使用构造器
  String s1 = new String(stringBuffer3)
  
  ```

### StringBuilder 类

- 通常适用在单线程中 

- 效率【StringBuilder > StringBuffer > String】

- 使用原则【String、StringBuffe、StringBuilder】

  ```
  1.如果字符串存在大量的修改操作，一般使用 StringBuffer 或 StringBuilder
  2.如果字符串存在大量的修改操作，并在单线程的情况，使用 StringBuilder
  3.如果字符串存在大量的修改操作，并在多线程的情况，使用 StringBuffer
  4.如果我们字符串很少修改，被多个对象引用，使用 String (比如配置信息等)
  ```

### Math 类

- Java之Math类使用小结：https://www.cnblogs.com/lukelook/p/11300890.html

### Arrays 类

- Java之Arrays类的方法小结：https://blog.csdn.net/weixin_41924879/article/details/100102009

#### sort排序详解

```java
//1.普通排序  
int[] arr = {1,5,6,8,9}
Arrays.sort(arr);  //默认升序


//sort 重载的，也可以传入一个接口 Comparator 实现定制排序
//2.定制排序    sort(T[] a,Comparator<? super T> c)
Arrays.sort(arr,new Comparator(){
    @Override
    public int compare(Object 01, Object o2){
        Integer i1 = (Integer) o1;
        Integer i2 = (Integer) o2;
        return i2 - i1; //这样子的返回，就是降序
    }
}); 

```

### System 系统类

- System类常用方法：https://www.cnblogs.com/yinzhengjie/p/8887145.html

### BigInteger和BigDecimal 类

- 应用场景

  ```
  BigInteger:适合保存比较大的整型
  BigDecimal:适合保存精度更高的浮点型(小数)
  ```

- Java之 BigInteger 类和 BigDecimal 类详解：https://blog.csdn.net/weixin_43767015/article/details/105129093

### Date 日期时间类

- 获取当前日期时间

  ```java
  /* 	Java中获取当前日期和时间很简单，使用 Date 对象的 toString() 方法来打印当前日期和时间，如下所示： */
  import java.util.Date;
    
  public class DateDemo {
     public static void main(String args[]) {
         // 初始化 Date 对象
         Date date = new Date(); //获取当前的时间
        //Date date1 = new Date(729993) 【Date()里面的可以输入毫秒数---->就可以输出毫秒数转换后的日期时间了】  
        
         // 使用 toString() 函数显示日期时间
         System.out.println(date.toString());
     }
  }

  ```

- SimpleDateFormat 格式化日期

  ```java
  /*	SimpleDateFormat 是一个以语言环境敏感的方式来格式化和分析日期的类。SimpleDateFormat 允许你选择任何用户自定义日期时间格式来运行。例如：*/
  import  java.util.*;
  import java.text.*;
   
  public class DateDemo {
     public static void main(String args[]) {
   
        Date dNow = new Date( );
        SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd hh:mm:ss");
   
        System.out.println("当前时间为: " + ft.format(dNow));
     }
  }
  
  ```
  
- 新日期类

  ```java
  /* 	LocalDate(日期/年月日)   LocalTime(时间/时分秒)  LocalDateTime(日期时间/年月日时分秒)*/
  LocalDate  只包含日期，可以获取日期字段
  LocalTime  只包含时间，可以获取时间字段
  LocalDateTime  包含日期 + 时间，可以获取日期和时间字符
      
  //第三代日期的格式化日期
  /* 	DateTimeFormatter   【各个格式参数  需要查看jdk8 的文档】  */
  //里面的格式就相对自由
  DateTimeFormatter dtf = new DateTimeFormatter("yyyy年MM月ddd日  HH时mm分ss秒") 
      
  ```
  
- 解析字符串为时间

  ```java
  /*	SimpleDateFormat 类有一些附加的方法，特别是parse()
  它试图按照给定的SimpleDateFormat 对象的格式化存储来解析字符串。例如：*/
  
  import java.util.*;
  import java.text.*;
  
  public class DateDemo {
   
     public static void main(String args[]) {
        SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd"); 
   
        String input = args.length == 0 ? "1818-11-11" : args[0]; //
   
        System.out.print(input + " Parses as "); 
   
        Date t; 
   
        try { 
            t = ft.parse(input); 
            System.out.println(t); 
        } catch (ParseException e) { 
            System.out.println("Unparseable using " + ft); 
        }
     }
  }
  
  ```


#### Calendar 日历类

```java
Calendar c = Calendar.getInstance(); //创建日历对象
System.out.println("c = " + c);

//格式化日期  月
System.out.println("月: " + c.get(Calendar.MONTH));
```



## 集合

### 知识体系图

![image.png](https://i.loli.net/2021/11/25/FJ3xnlNHWTkGPvo.png)

### 集合框架体系

- 说明

  ```java
  集合主要是两组(单列集合、双列集合)
  Collection 接口有两个重要的子接口 List Set , 他们的实现子类都是单列集合
  Map 接口的实现子类 是 双列集合，存放的 K-V
  ```
  
- 类图

  (1)单列集合

  ![image.png](https://i.loli.net/2021/11/26/IpkoXazSDjqT2Ol.png)

  (2)双列集合

  ![image.png](https://i.loli.net/2021/11/25/z5bLhye1aGQCpVX.png)

### Collection 接口

#### 常用方法

```
(1)add 添加单个元素
(2)remove 删除指定元素
(3)contains 查找元素是否存在
(4)size 获取元素个数
(5)isEmpty 判断是否为空
(6)clear 清空
(7)addAll 添加多个元素
(8)containsAll 查找多个元素是否都存在
(9)removeAll 删除多个元素
(10)说明:可以用ArrayList实现类来操作
```

#### 遍历元素方式

- **Iterator 迭代器** 【方式一】

  ```
  (1)Iterator 对象称为迭代器，主要用于遍历 Collection 集合中的元素
  (2)所有实现了Collection 接口的集合类都有一个iterator()方法，用于返回一个实现了 Iterator 对象，即返回一个迭代器
  (3)Iterator 结构图
  (4)Iterator 仅用于遍历集合，Iterator 本身并不存放对象
  ```

- **增强for循环（foreach）**【方式二】

  ```
  for语句的增强，使得对于集合和数组的遍历更简便
  //快捷键--->itit
  形式举例:
  for(char ch:chars){//其中char-->数据类型 ch--->单个遍历存放变量  chars--->数组名
   	...
  }
  ```

- **普通for循环**【方式三】

- 实例

  ```java
  // 引入 ArrayList 和 Iterator 类  
  
  /*	迭代器 it 的3个基本操作是 next 、hasNext 和 remove。
  调用 it.next() 会返回迭代器的下一个元素，并且更新迭代器的状态。
  调用 it.hasNext() 用于检测集合中是否还有元素。
  调用 it.remove() 将迭代器返回的元素删除。
   */
      
  import java.util.ArrayList;
  import java.util.Iterator;
  
  public class RunoobTest {
      public static void main(String[] args) {
  
          // 创建集合
          ArrayList sites = new ArrayList();
          sites.add("苹果");
          sites.add("香蕉");
          sites.add("桃子");
          sites.add("西瓜");
  
          // 获取迭代器
          Iterator it = sites.iterator();
  
          // 输出集合中的第一个元素
          System.out.println(it.next());
          
          // 输出集合中的所有元素  Iterator迭代器的使用
          //IDEA中 快速生成while快捷键  => itit
          while(it.hasNext()) {
              System.out.println(it.next());
          }
          //增强for循环【foreach】
          for (Object obj:sites) {
              System.out.println(obj);
          }
      }
  }
  
  ```

#### List 子接口和实现类

- 基本介绍

  ```
  List 接口是 Collection 接口的子接口
  (1)List集合类中元素有序(即 添加顺序和取出顺序一致)、且可重复
  (2)List集合类中的每个元素都有其对应的顺序索引，即支持索引
  (3)List容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素
  (4)JDK API中List接口的实现类 【常用的有 ArrayList、LinkedList 和 Vector】
  
  ```

##### ArrayList 类 

- ArrayList 底层结构和源码分析（！！！！）

  ```
  (1)ArrayList中维护了一个Object类型的数组elementData
  	transient Object[] elementData; //transient(瞬间、短暂的) 表示该属性不会被序列化
  (2)当创建ArrayList对象时，如果使用的是无参构造器，则初始elementData容量为0，第1次添加，则扩容elementData为10，如需要再次扩容，则扩容elementData为1.5倍
  (3)如果使用的是指定大小的构造器，则初始elementData容量为指定大小，如果需要扩容，则直接扩容elementData为1.5倍。
  
  ```

- 使用ArrayList 情况

  ```
  (1)频繁访问列表中的某一个元素
  (2)只需要在列表末尾进行添加和删除元素操作
  ```

- 添加、删除、修改、遍历等功能

  ```java
  import java.util.ArrayList;
  public class Test02 {
      public static void main(String[] args) {
          ArrayList<String> sites = new ArrayList<String>();
          //添加
          sites.add("苹果");
          sites.add("香蕉");
          sites.add("桃子");
          sites.add("西瓜");
          System.out.println(sites);
          //获取
          System.out.println(sites.get(1));
          //修改
          sites.set(2,"西红柿炒蛋");
          System.out.println(sites);
          //删除
          sites.remove(3);
          System.out.println(sites);
          //计算大小
          System.out.println(sites.size());
          //迭代 1.for循环
          for (int i = 0; i < sites.size() ; i++){
              System.out.println(sites.get(i));
          }
          //迭代 2.for-each循环
          for (String i:sites){
              System.out.println(i);
          }
      }
  }
  ```
  
- ArrayList 的部分方法  

  ```java
  方法         描述
  add()	将元素插入到指定位置的 arraylist 中
  addAll()	添加集合中的所有元素到 arraylist 中
  clear()	删除 arraylist 中的所有元素
  clone()	复制一份 arraylist
  contains()	判断元素是否在 arraylist
  get()	通过索引值获取 arraylist 中的元素
  indexOf()	返回 arraylist 中元素的索引值
  removeAll()	删除存在于指定集合中的 arraylist 里的所有元素
  remove()	删除 arraylist 里的单个元素
  size()	返回 arraylist 里元素数量
  isEmpty()	判断 arraylist 是否为空
  subList()	截取部分 arraylist 的元素  
  set()	替换 arraylist 中指定索引的元素
  sort()	对 arraylist 元素进行排序
  toArray()	将 arraylist 转换为数组
  toString()	将 arraylist 转换为字符串
  ensureCapacity()	设置指定容量大小的 arraylist
  lastIndexOf()	返回指定元素在 arraylist 中最后一次出现的位置
  retainAll()	保留 arraylist 中在指定集合中也存在的那些元素
  containsAll()	查看 arraylist 是否包含指定集合中的所有元素
  trimToSize()	将 arraylist 中的容量调整为数组中的元素个数
  removeRange()	删除 arraylist 中指定索引之间存在的元素
  replaceAll()	将给定的操作内容替换掉数组中每一个元素
  removeIf()	删除所有满足特定条件的 arraylist 元素
  forEach()	遍历 arraylist 中每一个元素并执行特定操作
      
  ```
  

##### LinkedList 类

- 使用LinkedList 情况

  ```
  你需要通过循环迭代来访问列表中的某些元素。
  需要频繁的在列表开头、中间、末尾等位置进行添加和删除元素操作
  ```

- 实例

  ```java
  import java.util.LinkedList;
  
  public class Test02 {
      public static void main(String[] args) {
          LinkedList<String> lind = new LinkedList<String>();
          lind.add("西红柿炒蛋");
          lind.add("凉拌黄瓜");
          lind.add("辣椒炒肉");
          System.out.println(lind);
          //头部添加
          lind.addFirst("煎蛋");
          System.out.println(lind);
          //尾部添加
          lind.addLast("鸡排");
          System.out.println(lind);
          //移除头部元素
          lind.removeFirst();
          System.out.println(lind);
          //移除尾部元素
          lind.removeLast();
          System.out.println(lind);
  
          //循环遍历
          for (int i=0; i <lind.size();i++){
              lind.removeLast();
              if (i == 2){
                  break;
              }
          }
          System.out.println(lind);
      }
  }
  
  ```

- LinkedList 常用方法  查类图或API文档

##### Vector 类

- Vector 底层结构和源码分析

  ```
  (1)Vector底层也是一个对象数组，protected Object[] elementData;
  (2)Vector 是线程同步的，即线程安全，Vector类的操作方法带有synchronized
  (3)在开发中，需要线程同步安全时，考虑使用Vector
  
  ```

#### Set 子接口和实现类

> 注：用法同 List接口 ，区别在于 Set接口 不可添加重复元素。

- 基本介绍

  ```
  (1)无序(添加和取出的顺序不一致)，没有索引 【取出的顺序虽然不是添加时顺序，但顺序是固定的】
  (2)不允许重复元素，最多包含一个null
  (3)JDK API 中Set接口的是实现类 【常用:HashSet 、TreeSet】
  
  ```

##### HashSet 类 

```
(1)实现了Set接口
(2)HashSet底层是HashMap，HashMap底层是（数组+链表+红黑树）
(3)用HashSet需要重写 equals() 和 hashCode()
(4)也需要知道有LinkedHashSet (链表的HashSet)
```

```java
//实例
package com.javaDemo.hashset_;

import java.util.HashSet;
import java.util.Objects;

@SuppressWarnings({"all"})
public class HashSetExercise {
    public static void main(String[] args) {
        HashSet hashSet = new HashSet();
        hashSet.add(new Employee("tom",20));
        hashSet.add(new Employee("jack",35));
        hashSet.add(new Employee("jack",35));

        System.out.println("=======员工列表=========");
        for (Object o :hashSet) {
            System.out.println(o);
        }

    }
}

class Employee{
    private String name;
    private int age;

    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    //如果 name 和 age 的equals()方法返回为 true 时
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return age == employee.age && Objects.equals(name, employee.name);
    }
	//则返回相同的 hashCode 值
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}

```

##### TreeSet 类

大同小异

### Map 接口和实现类 

- 基本介绍

  ```
  (1)Map与Collection并列存在。用于保存具有映射关系的数据:Key-Value(双列元素)
  (2)Map 中的 Key 和 Value 可以是任何引用类型的数据，会封装到HashMap$Node 对象中
  (3)Map 中的 Key 不允许重复，原因和HashSet 一样，前面分析过源码
  (4)Map 中的 Vaule 可以重复
  
  ```

- Map接口常用方法

  ```
  put(Object key,Object value)和putAll(Collection c)  添加映射(单个和全部)
  get(Object key)  根据键来获取对应的值
  containsKey(Object key)和containsValue(Object value) 查找 键 和 值 是否存在
  remove(Object key) 根据键删除映射关系
  size() 获取元素个数
  values() 返回映射中所有 value 组成的 Set 视图 【可以通过迭代(hashMap.values)遍历 值】
  keySet() 返回映射中所有 key 组成的 Set 视图 【可以用来遍历 键】
  entrySet() 方法返回映射中包含的映射的 Set 视图 【遍历返回的是全部 键=值 】
  isEmpty()  判断个数是否为0
  
  ```

#### Map遍历方式

```
//迭代器遍历
HashMap  hashMap = new HashMap();  //这里是不加泛型的遍历 key-v
Iterator iterator = hashMap.entrySet().iterator();
while (iterator.hasNext()) {
    Map.Entry entry = (Map.Entry) iterator.next();
    System.out.println(entry.getKey() + "----" + entry.getValue());
}
        
```

#### HashMap 类

- 基本介绍

  ```java
  HashMap 是 Map的实现类 使用最广泛
  HashMap没有实现同步，因此是线程不安全的
  ```
  
- 实例

  ```java
  /*基本用法和 ArrayList 一样，删除和修改只需要找到对应的键删除就可以，键对应的值随之删除。
  */
  
  import java.util.HashMap;
  
  public class Test02 {
      public static void main(String[] args) {
          HashMap<Integer,String> hast = new HashMap<Integer,String>();
          //添加元素
          hast.put(1,"西红柿炒蛋");
          hast.put(2,"凉拌黄瓜");
          hast.put(3,"茶叶蛋");
          System.out.println(hast);
          //获取对应元素
          System.out.println(hast.get(2));
          //删除对应元素
          hast.remove(3);
          System.out.println(hast);
      }
  }
  
  ```

#### Hashtable 类

- 基本介绍

  ```
  (1)存放的元素是键值对：即K-V
  (2)Hashtable的键和值都不能为null
  (3)Hashtable使用方法基本上和HashMap一样
  (4)Hashtable是线程安全的，HashMap 是线程不安全的
  
  ```


##### Properties 类 

```
继承Hashtable并实现了Map接口，也是使用一种键值对的形式来保存数据
使用特点和Hashtable类似

```

实例

```java
package com.test.properties_;

import java.io.FileReader;
import java.io.IOException;
import java.util.Properties;

/**
 * 配置文件properties信息: 
 * name=tom
 * age=12
 * color=red
 * 演示 读取 properties 中的对象
 */
public class Properties01 {
    public static void main(String[] args) throws IOException {
        String filePath = "src\\dog.properties";
        Properties properties = new Properties();
        properties.load(new FileReader(filePath));
        String name = properties.get("name") + "";
        int age = Integer.parseInt(properties.get("age") + "");
        String color = properties.get("color") + "";

        Dog dog = new Dog(name,age,color);
        System.out.println(dog);

    }
}

class Dog{
    private String name;
    private int age;
    private String color;

    public Dog(String name, int age, String color) {
        this.name = name;
        this.age = age;
        this.color = color;
    }

    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", color='" + color + '\'' +
                '}';
    }
}

```



#### TreeMap 类

大同小异

### 如何选择集合实现类

```
(1)先判断存储的类型(一组对象或者一组键值对)
(2)一组对象：Collection接口
    允许重复：List
        增删多：LinkedList 【底层维护了一个双向链表】
        改查多：ArrayList 【底层维护 Object类型的可变数组】
    不允许重复：Set
        无序：HashSet 【底层是HashMap，维护了一个哈希表 (即:数组+链表+红黑树)】
        排序：TreeSet 
        插入和取出顺序一致：LinkedHahSet 【维护数组+双线链表】
(3)一组键值对：Map
    键无序：HashMap 【底层是 哈希表 jdk7：数组+链表， jdk8：数组+链表+红黑树】
    键排序：TreeMap
    键插入和去除顺序一致：LinkedHashMap
    读取文件：Properties
    
```

### Collections 工具类

- Collections工具类介绍

  ```
  Collections是一个操作 Set、List 和 Map 等集合的工具类
  Collections 中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作
  ```

- 排序操作：（均为static方法）

  ```
  (1)reverse(List) 反转List中元素的顺序
  (2)shuffle(List) 对List集合元素进行随机排序
  (3)sort(List) 根据元素的自然顺序对指定 List 集合元素按升序排序
  (4)sort(List,Comparator) 根据指定的 Comparator 产生的顺序对List集合元素进行排序
  (5)swap(List,int,int) 将指定List集合中的i处元素和j处元素进行交换
  
  ```

- 查找、替换

  ```
  (1)Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
  (2)Object max(Collection,Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
  (3)Object min(Collection)
  ()Object min(Collection,Comparator)
  ()int frequency(Collection,Object) 返回指定集合中元素的出现次数
  ()void copy(List dest,List src) 将src中的内容辅助到dest中
  ()boolean replaceAll(List list,Object oldVal,Object newVal) 使用新值替换 List 对象的所有旧值
  
  ```

## 泛型

> 泛(广泛)型(类型)： 代表一种数据类型   如:E  ==(代表)==>  Integer / String （其类型参数只能代表引用型类型）

### 泛型的介绍

- 泛型解读

  ```
  (1)泛型又称参数化类型，是jdk5.0 出现的新特性，解决数据类型的安全问题
  (2)在类声明或者实例化时只要指定好需要的具体类型即可
  (3)java泛型可以保证如果程序在编译时没有发出警告，运行时就不会产生ClassCastException异常。同时，代码更加简洁、健壮
  (4)泛型的作用是：可以在类声明时通过一个标志表示类中某个属性的类型，或者是某个方法的返回值的类型，或者是参数类型 
  【其中 E 具体的数据类型在定义对象时指定，即在编译期间，就确定 E 时什么类型 (不明白参考:https://www.bilibili.com/video/BV1fh411y7R8?p=556) 】
  
  ```

- 泛型的声明

  ```
  interface 接口<T>{} 和 class类<K,V>{}
  比如：List,ArrayList
  说明:
  (1)其中 T,K,V不代表值，而是表示类型
  (2)任意字母都可以。常用T表示，(Type的缩写)
  
  ```

- 泛型的实例化

  ```
  要在类名后面指定数据类型参数的值(类型) 。如：
  (1)List<String> strList = new ArrayList<String>();
  (2)Iterator<Customer> iterator = customers.iterator();
  
  ```
  

### 泛型经典案例

```
题目要求：
(1)定义一个y该类包含:private成员变量name,sal,birthday,其中 birthday 为 MyDate类的对象;
(2)为每一个属性定义getter, setter方法;
(3)重写toString方法输出name, sal, birthday
(4) MyDate类包含:private成员变量month,day,year;并为每一个属性定义getter,setter方法;
(5)创建该类的3个对象,并把这些对象放入ArrayList 集合中(ArrayList需使用泛型来定义)，对集合中的元素进行排序,并遍历输出:
	排序方式:调用ArrayList 的sort方法，传入Comparator对象[使用泛型],先按照name排序,如果name相同，则按生日日期的先后排序。【即:定制排序】

```

**（1）GenericHomework01.java**

```java
package com.stage_homework.generic;

import java.util.ArrayList;
import java.util.Comparator;

@SuppressWarnings({"all"})
public class GenericHomework01 {
    public static void main(String[] args) {
        ArrayList<Employee> employees = new ArrayList<>();
        employees.add(new Employee("tom", 18000, new MyDate(2000, 11, 3)));
        employees.add(new Employee("jack", 30000, new MyDate(1990, 11, 15)));
        employees.add(new Employee("mary", 2500, new MyDate(1998, 11, 8)));
        employees.add(new Employee("mary", 2500, new MyDate(1997, 11, 8)));
        employees.add(new Employee("mary", 2500, new MyDate(1998, 11, 9)));

        System.out.println("========初始员工列表=========");
        for (Employee employee : employees) {
            System.out.println(employee);
        }

        // 对员工进行排序
        employees.sort(new Comparator<Employee>() {  //Comparator接口  所以可以使用匿名内部类
            @Override
            public int compare(Employee emp1, Employee emp2) {
                //传入Comparator对象[使用泛型],先按照name排序,如果name相同，则按生日日期的先后排序。【即:定制排序】
                //先判断o1,o2是否为mull,如果是，则不比
                if (!(emp1 instanceof Employee && emp2 instanceof Employee)) {
                    System.out.println("类型不匹配...");
                    return 0;
                }
                //先比较name
                int i = emp1.getName().compareTo(emp2.getName());
                if (i != 0){ //名字不相同
                    return i;
                }

                //比较birthday
                return emp1.getBirthday().compareTo(emp2.getBirthday());
            }
        });

        System.out.println("=========排序后结果======");
        for (Employee employee :employees) {
            System.out.println(employee);
        }

    }
}

```

**（2）Employee.java**

```java
package com.stage_homework.generic;

public class Employee {
    private String name;
    private double sal;
    private MyDate birthday;

    public Employee(String name, double sal, MyDate birthday) {
        this.name = name;
        this.sal = sal;
        this.birthday = birthday;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSal() {
        return sal;
    }

    public void setSal(double sal) {
        this.sal = sal;
    }

    public MyDate getBirthday() {
        return birthday;
    }

    public void setBirthday(MyDate birthday) {
        this.birthday = birthday;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", sal=" + sal +
                ", birthday=" + birthday +
                '}';
    }
}

```

**（3）MyDate.java**

```java
package com.stage_homework.generic;

public class MyDate implements Comparable<MyDate>{ 
    private int year;
    private int month;
    private int day;

    public MyDate(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public int getMonth() {
        return month;
    }

    public void setMonth(int month) {
        this.month = month;
    }

    public int getDay() {
        return day;
    }

    public void setDay(int day) {
        this.day = day;
    }

    @Override
    public String toString() {
        return year + "-" + month + "-" + day;
    }

    @Override
    public int compareTo(MyDate o) {
        //再比较生日
        //name相同就比较year
        int yearMinus = year - o.getYear();
        if (yearMinus != 0){
            return yearMinus;
        }
        //year相同就比较month
        int monthMinus = month - o.getMonth();
        if (monthMinus != 0){
            return monthMinus;
        }
        //month相同就比较day
        int dayMinus = day - o.getDay();
        return dayMinus;
    }
    
}

```

### 自定义泛型

#### 自定义泛型类

```
//基本语法
class 类名 <T,R...>{

}

//注意细节
(1)普通成员可以使用泛型(属性、方法)
(2)使用泛型的数组，不能初始化
(3)静态方法中不能使用类的泛型
(4)泛型类的类型，是在创建对象时确定的 (因为创建对象时，需要指定确定类型) 【属性时在类加载时就确定了，所以说不能使用泛型】
(5)如果在创建对象时，没有指定类型，默认为Object

```

```
java 中泛型标记符：

E - Element (在集合中使用，因为集合中存放的是元素)
T - Type（Java 类）
K - Key（键）
V - Value（值）
N - Number（数值类型）
？ - 表示不确定的 java 类型
```

#### 泛型方法实例

```java
public class Test02 {
    public static void main(String[] args) {
        //创建不同类型数组
        Integer[] intArray = {1,2,3,4,5};
        Double[] doubleArray = {1.2,2.3,2.1, 4.5};
        Character[] charArray = {'a','f','D','A','d'};
        
        System.out.println("整型数据：");
        printArray(intArray);
        System.out.println("精度型数据：");
        printArray(doubleArray);
        System.out.println("字符型数据：");
        printArray(charArray);
    }
    //定义 泛型方法 printArray
    public static <E> void printArray(E[] inputArray){
        //输出数组元素
        for (E element : inputArray){
            System.out.printf("%s" , element);
        }
    }
    
}
```

#### 求三者中最大值 的实例

```java
// 求三者中最大值 的实例（类型不定）
public class MaximumTest{
   public static void main( String args[] ){
      System.out.printf( "%d, %d 和 %d 中最大的数为 %d\n\n",
                   3, 4, 5, maximum( 3, 4, 5 ) );
      System.out.printf( "%.1f, %.1f 和 %.1f 中最大的数为 %.1f\n\n",
                   6.6, 8.8, 7.7, maximum( 6.6, 8.8, 7.7 ) );
      System.out.printf( "%s, %s 和 %s 中最大的数为 %s\n","pear",
         "apple", "orange", maximum( "pear", "apple", "orange" ) );
   }
   // 比较三个值并返回最大值
   public static <T extends Comparable<T>> T maximum(T x, T y, T z){               
      T max = x; // 假设x是初始最大值
      if ( y.compareTo( max ) > 0 ){
         max = y; //y 更大
      }
      if ( z.compareTo( ma x ) > 0 ){
         max = z; // 现在 z 更大           
      }
      return max; // 返回最大对象
   }
}
/*输出结果：
3, 4 和 5 中最大的数为 5
6.6, 8.8 和 7.7 中最大的数为 8.8
pear, apple 和 orange 中最大的数为 pear
*/

```

#### 自定义泛型接口

```
//基本语法：
interface 接口名<T,R...>{

}
//注意细节
(1)接口中，静态成员也不能使用泛型(这个和泛型类规定一样)
(2)泛型接口的类型，在继承接口或者实现接口时确定
(3)没有指定类型，默认为Object
```

#### 自定义泛型方法

```java
//基本语法
class 类名 <T,R...>{
	public <K> void hello(T t, K k){ //指定什么类型就可以输出什么类型
		 System.out.println(t.getClass()); //前面创建对象时定义的什么类型，这里返回的就是什么数据类型
		  System.out.println(k.getClass());
	}
}

```

### 泛型的继承和通配符

- 说明

  ```
  (1)泛型不具备继承性
  	List<Object> list = new ArrayList<String>();//错的
  (2)<?>:支持任意泛型类型
  (3)<? extends A>:支持A类，以及A类的子类，规定了泛型的上限
  (4)<? super A>:支持A类，以及A类的父类，不限于直接父类，规定了泛型的下限
  
  ```

- 实例

  ```java
  /*类型通配符一般是使用 ? 代替具体的类型参数。例如 List<?> 在逻辑上是 List<String>,List<Integer> 等所有 List<具体类型实参> 的父类。
  */
  
  import java.util.*;
   
  public class GenericTest {
  
      public static void main(String[] args) {
          List<String> name = new ArrayList<String>();
          List<Integer> age = new ArrayList<Integer>();
          List<Number> number = new ArrayList<Number>();
          
          name.add("icon");
          age.add(18);
          number.add(314);
   
          getData(name);
          getData(age);
          getData(number);
         
     }
   
     public static void getData(List<?> data) {
        System.out.println("data :" + data.get(0));
     }
  }
  ```

### JUnit使用

- 基本介绍

  ```
  (1)JUnit是以一个Java语言的单元测试框架
  (2)多数Java的开发环境都已经集成了JUnit作为单元测试的工具
  (3)在方法上面像使用注解一样添加 @Test ，第一次使用需要先引入  按Atr+Enter 选第二个JUnit.5.4 添加即可 【注：添加完成后 在IDEA中 对应的左边 将会出现绿色的运行标志】
  
  ```



## 异常处理

### 五大运行时异常

```
1.NullPointerException空指针异常【当应用程序试图在需要对象的地方使用null 时，抛出该异常】 
2.ArithmeticExcetion数学运算异常【当出现异常的运算条件时，抛出异常】
3.ArryIndexOutOfBoundsException数组下标越界异常【用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引】
4.ClassCastException类型转换异常【当试图将对象强制转换为不是实例的子类时，抛出该异常】
5.NumberFormatException数字格式不正常异常【当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常 ==> 使用异常我们可以确保输入是满足条件数字】

```

### 异常体系图

![image.png](https://i.loli.net/2021/11/24/oK72wdzsA6JkZhX.png)

- 捕获异常

  - 语法代码块

    ```java
    try
    {
       // 程序代码
    }catch(ExceptionName e1)
    {
       //Catch 块
    }
    
    ```

  - 实例

    ```java
    // 文件名 : ExcepTest.java
    import java.io.*;
    public class ExcepTest{
     
       public static void main(String args[]){
          try{
             int a[] = new int[2];
             System.out.println("Access element three :" + a[3]);
          }catch(ArrayIndexOutOfBoundsException e){
             System.out.println("Exception thrown  :" + e);
          }
          System.out.println("Out of the block");
       }
    }
    
    ```
    

- thorw/throws关键字

  ```java
  //throw 抛出异常  throws声明抛出异常
  import java.io.*;
  public class className
  {
    public void deposit(double amount) throws RemoteException
    {
      // Method implementation
      throw new RemoteException();
    }
    //Remainder of class definition
  }
  
  ```
  
- finally关键字

  ```java
  public class ExcepTest{
    public static void main(String args[]){
      int a[] = new int[2];
      try{
         System.out.println("Access element three :" + a[3]);
      }catch(ArrayIndexOutOfBoundsException e){
         System.out.println("Exception thrown  :" + e);
      }
      finally{
         a[0] = 6;
         System.out.println("First element value: " +a[0]);
         System.out.println("The finally statement is executed");
      }
    }
  }
  
  ```
  
- 声明自定义异常

  ```java
  // 文件名InsufficientFundsException.java
  import java.io.*;
   
  //自定义异常类，继承Exception类
  public class InsufficientFundsException extends Exception
  {
    //此处的amount用来储存当出现异常（取出钱多于余额时）所缺乏的钱
    private double amount;
    public InsufficientFundsException(double amount)
    {
      this.amount = amount;
    } 
    public double getAmount()
    {
      return amount;
    }
  }
  ```

  

## 多线程

### 基本介绍

进程开启的  主线程、子线程 还可以开启一个线程

![image.png](https://i.loli.net/2021/12/01/FWhAKYM4nIX9Jj6.png)



```
 t.start();//开启线程
 
 t.sleep(); //休眠
 
 //线程的插队：插队的线程一旦插队成功，则肯定先执行完插入的线程所有的任务。
 t.join(); 
 
//线程的礼让：让出cpu，让其他线程执行，但礼让的时间不确定，所以也不一定礼让成功
 t.yield(); 
 
```

### 线程的生命周期

#### 线程状态转换图

![image.png](https://i.loli.net/2021/12/02/G6mcAYqWM12pXPF.png)



### Synchroized 

#### 线程同步机制

1.在多线程编程，一些敏感数据不允许被多个线程与同时访问，此时就是用同步访问技术，保证数据在任何情况下，最多有一个线程访问，以保证数据的完整性。

2.也可以这样理解：线程同步，即当一个线程对内存进行操作时，其他线程都不可以对这个内存地址进行操作，直到该线程完成操作，其他线程才能对该内存地址进行操作。

- 同步具体方法

  ```
  1.同步代码块
  synchronized(){ //得到对象的锁，才能操作同步代码
  	//需要被同步代码;
  }
  
  2.synchronized 还可以放在方法体声明中，表示整个方法--为同步方法
  public synchronized void m(String name){
  	//需要被同步代码;
  }
  
  ```

### 锁

- 互斥锁

  ```
  一般都是加在代码块中 ( ) --> 可以时this，也可以是任意对象
  synchronized(this){ //得到对象的锁，才能操作同步代码
  	//需要被同步代码;
  }
  
  实现的步骤：
  首先需要先分析上锁的代码
  选择同步代码块或同步方法
  要求多个线程的锁对象为同一个即可！
  
  ```

- 死锁

  > 注意避免死锁！！

- 释放锁



### 两种创建的方式

#### 继承 Thread 

> 继承 Thread 类【重点】

- 实例

  ```java
  //创建线程方式一：继承Thread 类 ，重写run() 方法 ，调用start开启线程
  public class Test02 extends Thread{
      public void run(){
          //run()方法线程体
         
          for (int i = 0; i < 20; i++) {
              System.out.println(i+"我在写代码------");
          }
      }
      public static void main(String[] args) {
          //main线程，主线程
          Test02 t = new Test02();
          t.start();//开启线程
          //t.run(); //调用run方法
          
          //主线程中关闭子线程
          
          for (int i = 0; i < 20; i++) {
              System.out.println(i+"我在吃饭-----");
          }
      }
  }
  
  ```


#### Runnable 接口 

> 实现 Runnable 接口 ----重点   【建议使用】

- 优点：避免单继承的局限性，灵活方便，方便同一个对象被同一个线程使用

- 实例  

  ```java
  /*	创建线程方式2：实现runnable 接口，重写run 方法，执行线程需要丢入runnable接口实现类，调用start方法   */
  
  public class TestThread1 implements Runnable{
      public void run(){
          //run方法线程体
          for (int i = 0; i < 200; i++) {
              System.out.println("我在学习------");
          }
      }
  
      public static void main(String[] args) {
          //创建runnable 接口的实现类对象
          TestThread1 t1 = new TestThread1();
  
          new Thread(t1).start(); //调用线程z
          
          for (int i = 0; i < 200; i++) {
              System.out.println("我在吃饭-----");
          }
      }
      
  ```
  

#### 

### 线程的其他相关概念

#### 并发

```
同一个时刻，多个任务交替执行，造成一种“貌似同时”的错觉，简单的说单核cpu实现的多任务就是并发

```

#### 并行

```
同一个时刻，多个任务同时执行，多核cpu可y实现并行
```



## IO流

### IO流体系图

![image.png](https://i.loli.net/2021/11/28/w7tRjg8Wi9ux2VF.png)

### 常见的文件操作

> 所有的操作都是对内存的操作，对文件读写可自动创建文件。

<img src="https://s2.loli.net/2021/12/04/ADsplm7MLS5E9Ug.png" alt="image.png" style="zoom: 80%;" />

#### 创建文件对象相关构造器和方法

```
new File(String pathname)  //根据路径构建一个File对象
new File(File parent,String child)  //根据父目录文件 + 子路径构建
new File(String parent,String child)  //根据父目录  + 子路径构建

createNewFile  创建新文件
```

- 创建文件方法

  ```java
  package com.test.writer;
  
  import java.io.File;
  import java.io.IOException;
  
  public class FileWriter {
      public static void main(String[] args) {
          fileWriter01(); 
      }
  
      public static void fileWriter01(){
          String pathName = "D:\\test.txt";
          File file = new File(pathName);  //这里创建对象只是把文件创建在内存
          try {
              file.createNewFile();   //真正的创建文件
              System.out.println("创建成功！");
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  
  ```

### 目录操作

- **mkdir**( ) 方法创建一个文件夹，成功则返回true，失败则返回false。失败表明File对象指定的路径已经存在，或者由于整个路径还不存在，该文件夹不能被创建。【一个目录】

- **mkdirs**() 方法创建一个文件夹和它的所有父文件夹。【多级目录】

#### 创建目录

```java
/*文件名 CreateDir.java*/
import java.io.File;
 
public class CreateDir {
    public static void main(String[] args) {
        String dirname = "/tmp/user/java/bin";
        File d = new File(dirname);
        // 现在创建目录
        d.mkdirs();
    }
}

```

#### 读取目录

```java
import java.io.File;
 
public class DirList {
    public static void main(String args[]) {
        String dirname = "/tmp";
        File f1 = new File(dirname);
        if (f1.isDirectory()) {
            System.out.println("目录 " + dirname);
            String s[] = f1.list();
            for (int i = 0; i < s.length; i++) {
                File f = new File(dirname + "/" + s[i]);
                if (f.isDirectory()) {
                    System.out.println(s[i] + " 是一个目录");
                } else {
                    System.out.println(s[i] + " 是一个文件");
                }
            }
        } else {
            System.out.println(dirname + " 不是一个目录");
        }
    }
}

/*输出结果：
目录 /tmp
bin 是一个目录
lib 是一个目录
demo 是一个目录
test.txt 是一个文件
README 是一个文件
index.html 是一个文件
include 是一个目录
*/

```

#### 删除目录或者文件

```java
/* 	删除文件可以使用 java.io.File.delete() 方法*/

import java.io.File;
 
public class DeleteFileDemo {
    public static void main(String[] args) {
        // 这里修改为自己的测试目录
        File folder = new File("/tmp/java/");
        deleteFolder(folder);
    }
 
    // 删除文件及目录
    public static void deleteFolder(File folder) {
        File[] files = folder.listFiles();
        if (files != null) {
            for (File f : files) {
                if (f.isDirectory()) {
                    deleteFolder(f);
                } else {
                    f.delete();
                }
            }
        }
        folder.delete();
    }
}


```

### 读写文件【都是对内存的操作】

#### FileInputStream【字节流输入】

- 使用字符串类型的文件名来创建一个输入流对象来读取文件

  ```java
  InputStream f = new FileInputStream("C:/java/hello");
  ```

- 使用一个文件对象来创建一个输入流对象来读取文件

  ```java
  File f = new File("C:/java/hello");
  InputStream in = new FileInputStream(f);
  ```

##### FileInputStream 实例

```java
package com.test.file;

import java.io.*;

public class File01 {
    public static void main(String[] args) {
         readFile01();
    }

    public static void readFile01() {
        String pathName = "D:\\hello.txt";
        int readData = 0;
        FileInputStream fileInputStream = null;
       
        try {
            //创建一个 FileInputStream 对象 用来读取文件
            fileInputStream = new FileInputStream(pathName);
            //从该输入流读取一个字节，数据，如果没有输入可用，则该方法被阻止

            while ((readData = fileInputStream.read()) != -1) {
                System.out.print((char) readData);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```

#### FileOutputStream【字节流输出】

- 使用字符串类型的文件名来创建一个输出流对象

  ```java
  OutputStream f = new FileOutputStream("C:/java/hello")
  ```

- 使用一个文件对象来创建一个输出流来写文件

  ```java
  File f = new File("C:/java/hello");
  OutputStream fOut = new FileOutputStream(f);
  
  ```
  

##### FileOutputStream 实例

```java
package com.test.file;

import java.io.*;

public class File01 {
    public static void main(String[] args) throws IOException {
        OutFile01();
    }

    public static void OutFile01() {
        String pathName = "D:\\hello.txt";
        int readData = 0;
        FileOutputStream fileOutputStream = null;
        try {
            fileOutputStream = new FileOutputStream(pathName);
            //写入一个字符
            String str = "Hello World!";
            fileOutputStream.write(str.getBytes());  //可以把一个字符串转换成一个bate数组


        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fileOutputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```

#### FileReader【字符流输入】

- 常用方法

  ```
  (1)new FileReader(File/String)
  (2)read:每次读取单个字符，返回该字符，如果到文件末尾返回-1
  (3)read(char[]):批量读取多个字符到数组，返回读取到的字符数，如果到文件末尾返回-1
  
  ```

- 相关API

  ```
  (1)new String(char[]):将char[] 转换成String
  (2)new String(char[],off,len):将char[] 的指定部分转换成String  //意思是从下标为0开始读len长度
  ```

##### FileReader 实例

```java
package com.test.reader;

import java.io.FileReader;
import java.io.IOException;

public class FileReader01 {
    public static void main(String[] args) {
        //fileReader01();
        fileReader02();
    }

    /**
     * 单个字符 读取文件
     */
    public static void fileReader01() {
        String str = "D:\\hello.txt";
        FileReader fileReader = null;
        int data = 0;

        try {
            fileReader = new FileReader(str);

            //1.循环读取 使用read() 单个字符读取
            while ((data = fileReader.read()) != -1) {
                System.out.print((char) data);
            }
            System.out.println("读取成功！");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fileReader != null) {
                try {
                    fileReader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    /**
     * 使用字符数组 读取文件
     */
    public static void fileReader02() {
        String str = "D:\\hello.txt";
        FileReader fileReader = null;

        int readLine = 0; //文件读取的长度
        char[] buf = new char[8];  //每次读取的字符

        try {
            fileReader = new FileReader(str);

            //1.循环读取 使用 read(char[]) 返回的是实际读取到的字符数
            //如果返回-1 即读到了文件末尾
            while ((readLine = fileReader.read(buf)) != -1) {
                System.out.print(new String(buf, 0, readLine));
            }
            System.out.println("读取成功！");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fileReader != null) {
                try {
                    fileReader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    
}

```

#### FileWriter【字符流输出】

> 注意：FileWriter使用后，必须要关闭(Close) 或刷新(flush)，否则写入不到指定文件！！！

- 常用方法

  ```
  (1)new FileWriter(File/String):覆盖模式，相当于流的指针在首端
  (2)new FileWriter(File/String,true):追加模式，相当于流的指针在尾端
  (3)Write(int):写入单个字符
  (4)Write(char[]):写入指定数组
  (5)Write(char[],off,len):写入指定数组的指定部分
  (6)Write(String):写入整个字符串
  (7)Write(String.off,len):写入字符串的指定部分
  ```

- 相关API

  ```
  String类：toCharSrray:将String转换成char[]
  ```

##### FileWriter 实例

```java
package com.test.writer;

import java.io.FileWriter;
import java.io.IOException;

public class FileWriter_ {
    public static void main(String[] args) {
        fileWriter01();
    }

    public static void fileWriter01() {
        String filePath = "D:\\test.txt";
        FileWriter fileWriter = null;
        char[] chars = {'a', 'b', 'c', 'd'};
        try {
            fileWriter = new FileWriter(filePath);
//            (3)Write(int):写入单个字符
            fileWriter.write('P');
//            (4)Write(char[]):写入指定数组
            fileWriter.write(chars);
//            (5)Write(char[],off,len):写入指定数组的指定部分
            fileWriter.write("我的家乡 1236".toCharArray(),0,6);
//            (6)Write(String):写入整个字符串
            fileWriter.write(" 你好 北京!");
//            (7)Write(String.off,len):写入字符串的指定部分
            fileWriter.write(" 上海 天津",0,3);
            System.out.println("写入成功！");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fileWriter.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```

### 节点流和处理流

#### 处理流

> 1.是一个包装类，它可以包装字符流，将字符流放入缓存里，先把字符读到缓存里，到缓存满了或者你flush的时候，再读入内存，就是为了提供读的效率而设计的。
>
> 2.BufferedReader 和 BufferedWriter 属于 字符流，是按照 字符 来读取数据的。.所以不要去操作 二进制文件【声音、视频、doc、ppt等】，可能造成文件的损坏。
>
> 3.操作 二进制文件【声音、视频、doc、ppt等】使用 BufferedInputStream  和 BufferedOutputStream 。
>
> 4.关闭时，只需要关闭外层流即可。 

##### BufferedReader  和 BufferedWriter 实例

```java
package com.test.bufferedreader_bufferedwriter;

import java.io.*;

public class BufferedReader_ {
    public static void main(String[] args) throws IOException {
//        bufferedReader_();
        bufferedWriter_();
    }


    public static void bufferedWriter_() throws IOException {
        String pathName = "D:\\test.txt";
        BufferedWriter bufferedWriter = new BufferedWriter(
                new FileWriter(pathName, true));  //这里可以设置字节流的追加 因为 BufferedWriter 没有追加方式

        String str = "123 我是谁？";
        String str1 = "123 我是谁？";
        String str2 = "123 我是谁？";

        bufferedWriter.write(str);
        bufferedWriter.newLine();
        bufferedWriter.write(str1);
        bufferedWriter.newLine();
        bufferedWriter.write(str2);
        bufferedWriter.newLine();

        System.out.println("写入成功！！");
        bufferedWriter.close();

    }

    public static void bufferedReader_() throws IOException {
        String pathName = "D:\\test.txt";
        BufferedReader bufferedReader = null;
        bufferedReader = new BufferedReader(new FileReader(pathName));
        String line;
        while ((line = bufferedReader.readLine()) != null) {
            System.out.println(line);
        }

        bufferedReader.close();
    }

}

```

##### BufferedInputStream  和 BufferedOutputStream 实例 

```java
package com.test.bufferedreader_bufferedwriter;

import java.io.*;

/**
 * bufferedInputStream 和 bufferedOutputStream 可以操作 二进制文件
 */
public class BufferedInputStream_ {
    public static void main(String[] args) {
        bufferedInputStream();
    }

    public static void bufferedInputStream(){  //文件的拷贝
        String srcFileName = "D:\\renew.jpg";
        String destFileName = "D:\\英雄时刻\\dest.jpg";
        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;
        int line = 0;
        byte[] bytes = new byte[1024];
        try {
            bis = new BufferedInputStream(new FileInputStream(srcFileName));
            bos = new BufferedOutputStream(new FileOutputStream(destFileName));

            while ((line = bis.read(bytes)) != -1){
                bos.write(bytes,0,line);
            }

            System.out.println("拷贝成功！！！");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (bis != null){
                    bis.close();
                }
                if (bos != null){
                    bos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    
}

```

##### 读取控制台输入

- BufferedReader 对象创建一个字符流  

  ```java
  BufferedReader br = new BufferedReader(new 
                        InputStreamReader(System.in));
  
  ```

- 多字符读取

  ```java
  //使用 BufferedReader 在控制台读取字符
   
  import java.io.*;
   
  public class BRRead {
      public static void main(String[] args) throws IOException {
          char c;
          // 使用 System.in 创建 BufferedReader
          BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
          System.out.println("输入字符, 按下 'q' 键退出。");
          // 读取字符
          do {
              c = (char) br.read();
              System.out.println(c);
          } while (c != 'q');
      }
  }
  
  /*输出结果：
  输入字符, 按下 'q' 键退出。
  runoob
  r
  u
  n
  o
  o
  b
  
  
  q
  q
  */
  
  ```

- 字符串读取

  ```java
  //使用 BufferedReader 在控制台读取字符
  import java.io.*;
   
  public class BRReadLines {
      public static void main(String[] args) throws IOException {
          // 使用 System.in 创建 BufferedReader
          BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
          String str;
          System.out.println("Enter lines of text.");
          System.out.println("Enter 'end' to quit.");
          do {
              str = br.readLine();
              System.out.println(str);
          } while (!str.equals("end"));
      }
  }
  
  /*输出结果：
  Enter lines of text.
  Enter 'end' to quit.
  This is line one
  This is line one
  This is line two
  This is line two
  end
  end
  */
  
  ```

##### 控制台输出

```java
/*	控制台的输出由 print( ) 和 println() 完成。这些方法都由类 PrintStream 定义，System.out 是该类对象的一个引用。PrintStream 继承了 OutputStream类，并且实现了方法 write()。*/

import java.io.*;
 
//演示 System.out.write().
public class WriteDemo {
    public static void main(String[] args) {
        int b;
        b = 'A';
        System.out.write(b);
        System.out.write('\n');
    }
}

```

#### 对象的序列化与反序列化 

- 序列化步骤

  1、创建一个对象输出流，他可以包装到一个其他类型的输出流，比如文件输出流：

  ```java
  ObjectOutputStream out = new ObjectOutputStream(
      new fileOutputStream("D:\\objectFile.obj"));
  ```

  2、通过对象输出流的 writeObject() 方法写对象：

  ```java
  out.writeObject("Hello");
  out.writeObject(new Date());
  ```

- 反序列化步骤

  1、创建一个对象输入流，他可以包装到一个其他类型的输出流，比如文件输入流：

  ```java
  ObjectInputStream out = new ObjectInputStream(
      new fileInputStream("D:\\objectFile.obj"));
  ```

  2、通过对象输入流的 readObject() 方法读取对象：

  ```java
  String obj1 = (String)out.readObject();
  Date obj2 = (Date)out.readObject();
  
  ```

### 

## 注解 

- 什么是注解？
  - Annotation作用：
    - 可以被其他程序（比如：编译器等）读取
  - Annotation的格式：
    - 注解是以“@注释名”在代码中存在的，还可以添加一些参数值，例如：@SuppressWarings(value="unchecked")。
  - Annotation在哪里使用：
    - 可以附加在package,class,method,field等上面，相当于给他们添加了额外的辅助信息，我们可以通过反射机制编程实现对这些元数据的访问。

### 内置注解

- @Override （用来判断下面的方法是否是重写方法，如果返回类型，方法名或者方法参数与父类的方法不同，则该注解会报红）

  - 实例

    ```java
    /*子类重写父类或者接口的方法时，建议使用此注解*/
    
    //不使用注解的情况下
    package test;
    
    public class SuperOverride {
    	public void method() {
    		System.out.println("父类方法");
    	}
    }
    
    package test;
    //需要重写父类的method方法，但是子类写成Method了，
    //此时编译器就不会报错，你就没法发现：子类没有重写父类的method方法。
    
    public class SubOverride extends SuperOverride{
    	public void Method() {
    		System.out.println("子类方法");
    	}
    }
    
    package test;
    
    public class OverrideTest {
    	public static void main(String args[]) {
    		SuperOverride sover = new SubOverride();
    		sover.method();//输出：父类方法
    	}
    }
    ```

- @Deprecated

  - 此注解可以用来注解不再使用以及过时的类、方法、属性。如果代码使用了Deprecated注解的类、方法、属性，编译器会给出警告。

    使用@Deprecated建议使用对应的@deprecated JavaDoc符号说明这个类、方法、属性替代方案及原因。

- @SuppressWarings（抑制警告）

  - 抑制编译器生成警告信息。它修饰的元素为类、方法、方法参数、属性、局部变量。

    当方法调用过时的方法或进行不安全类型转换时，编译器会生成警告，此时可以为这个方法增加@SuppressWarnings注解。

  - 解读：

    ```
    当我们不希望看到这些警告信息的时候，可以使用 SuppressWarnings 注解来抑制警告信息
    在{""}中，可以写入你希望抑制(b)
    ```

    

### 自定义注解，元注解（了解即可）

- 元注解 （ 修饰注解的注解）

  - @Target ：（用于描述注解的范围，即注解在哪用）

    ```java
    /*
    它说明了Annotation所修饰的对象范围：Annotation可被用于 packages、types（类、接口、枚举、Annotation类型）、类型成员（方法、构造方法、成员变量、枚举值）、方法参数和本地变量（如循环变量、catch参数）等。取值类型（ElementType）有以下几种：
    
    　　1.	CONSTRUCTOR:用于描述构造器
    　　2.	FIELD:用于描述域即类成员变量
    　　3.	LOCAL_VARIABLE:用于描述局部变量
    　　4.	METHOD:用于描述方法
    　　5.	PACKAGE:用于描述包
    　　6.	PARAMETER:用于描述参数
    　　7.	TYPE:用于描述类、接口(包括注解类型) 或enum声明
    　　8.	TYPE_PARAMETER:1.8版本开始，描述类、接口或enum参数的声明
    　　9.	TYPE_USE:1.8版本开始，描述一种类、接口或enum的使用声明
    */
    @Target({ElementType.METHOD, ElementType.TYPE})
    public @interface Log {
        ......
    }
    ```

  - @Retention ：（用于描述注解的生命周期，表示需要在什么级别保存该注解，即保留的时间长短）

    ```java
    /*取值类型（RetentionPolicy）有以下几种：
    
    　　1.	SOURCE:在源文件中有效（即源文件保留）
    　　2.	CLASS:在class文件中有效（即class保留）
    　　3.	RUNTIME:在运行时有效（即运行时保留）
    */
    
    @Target({ElementType.METHOD, ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    public @interface Log {
    　　......
    }
    ```
  
  - @Documented ：(用于描述其它类型的annotation应该被作为被标注的程序成员的公共API，因此可以被例如javadoc此类的工具文档化)

    ```java
    /*	它是一个标记注解，没有成员	*/
    @Target({ElementType.METHOD, ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    public @interface Log {
    　　......
    }
    
    ```
  
  - @Inherited ：(用于表示某个被标注的类型是被继承的)

## 反射 (reflection) 【715集】

- 发射机制

  > 可以把方法视为对象(万物皆对象)

<img src="https://s2.loli.net/2021/12/11/S5xHuQjCeZBhXtE.png" alt="image.png" style="zoom:80%;" />



### 反射相关的类

> 1.java.lang.Class：代表一个类，Class对象表示某个类加载在堆中的对象
>
> 2.java.lang.reflect.Method：代表类的方法，Method对象表示某个类的方法
>
> 3.java.lang.reflect.Field：代表类的成员变量
>
> 4.java.lang.reflect.Constructor：代表类的构造方法

演示案例

<img src="https://s2.loli.net/2021/12/11/rZTLPz4S2Qku85j.png" alt="image.png" style="zoom:80%;" />









