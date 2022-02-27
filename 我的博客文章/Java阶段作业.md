---
title: Java阶段作业
date: 2021-12-10
tags: 
    - homework
    - 阶段性
    - Java
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。 

<!-- more -->

## 第一题 【Person类】

```
题目：
定义一个 Person 类{ name,age,job} ，初始化Person 对象数组，有3个person对象，并按照 age 从大到小进行排序， 排序使用冒泡排序

```

```java
package com.homework.Homework1;

/*要求：
 *  定义一个 Person 类{ name,age,job} ，初始化Person 对象数组，有3个person对象，并按照 age 从大到小进行排序， 排序使用冒泡排序
 * */

public class testPerson {
    public static void main(String[] args) {
        Person[] persons = new Person[3];
        persons[0] = new Person("tom", 20, "上班");
        persons[1] = new Person("jack", 21, "上班");
        persons[2] = new Person("lunar", 22, "上班");

        //原始信息
        for (int i = 0; i < persons.length; i++) {
            System.out.println(persons[i].toString());
        }
        System.out.println("======================================");
        //使用冒泡排序
        Person temp = null;
        for (int i = 0; i < persons.length - 1; i++) {
            for (int j = 0; j < persons.length - 1 - i; j++) {
                if (persons[j].getAge() < persons[j+1].getAge()){
                    temp = persons[j];
                    persons[j] = persons[j+1];
                    persons[j+1] = temp;
                }
            }
        }
        //输出排序后的结果
        for (int i = 0; i < persons.length; i++) {
            System.out.println(persons[i].toString());
        }
        
    }
}

class Person {
    private String name;
    private int age;
    private String job;

    public Person(String name, int age, String job) {
        this.name = name;
        this.age = age;
        this.job = job;
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

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", job='" + job + '\'' +
                '}';
    }
}

```



## 第二题 【访问修饰符 访问权限】

写出4种访问修饰符，并说明各自的访问权限

| 访问修饰符 | 同类 | 同包 | 子类 | 不同包 |
| :--------: | :--: | :--: | :--: | :----: |
|   public   |  √   |  √   |  √   |   √    |
| protected  |  √   |  √   |  √   |   ×    |
|    默认    |  √   |  √   |  ×   |   ×    |
|  private   |  √   |  ×   |  ×   |   ×    |



## 第三题【Teacher类 继承】

```
题目:编写老师类
(1)要求有属性 姓名{name}，年龄{age}，职称{post}，基本工资{salary}
(2)编写业务方法，introduce()，实现输出一个教师的信息
(3)编写教师类的三个子类：教授类(Professor)、副教授类、讲师类。工资级别分别为：教授为1.3、副教授为1.2、
讲师为1.2。在三个子类里面都重写父类的interface()方法。
(4)定义并初始化一个老师对象，调用业务方法，实现对象基本信息即可
```

- `Teacher` （老师类）

  ```java
  package com.homework.Homework3;
  
  /*
   * 编写老师类
   * (1)要求有属性 姓名{name}，年龄{age}，职称{post}，基本工资{salary}
   * (2)编写业务方法，introduce()，实现输出一个教师的信息
   * (3)编写教师类的三个子类：教授类(Professor)、副教授类、讲师类。工资级别分别为：教授为1.3、副教授为1.2、
   * 讲师为1.2。在三个子类里面都重写父类的interface()方法。
   * (4)定义并初始化一个老师对象，调用业务方法，实现对象基本信息即可
   * */
  public class Teacher {
      private String name;
      private int age;
      private String post;
      private double salary;
  
      public Teacher(String name, int age, String post, double salary) {
          this.name = name;
          this.age = age;
          this.post = post;
          this.salary = salary;
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
  
      public String getPost() {
          return post;
      }
  
      public void setPost(String post) {
          this.post = post;
      }
  
      public double getSalary() {
          return salary;
      }
  
      public void setSalary(double salary) {
          this.salary = salary;
      }
      //业务方法  输出基本信息
      public String introduce() {
          return "姓名：" + getName() + " 年龄：" + getAge() + " 职称：" + getPost() + " 基本工资：" + getSalary();
      }
  }
  ```

- `Professor` （教授类）

  ```java
  package com.homework.Homework3;
  
  public class Professor extends Teacher{
  
      public Professor(String name, int age, String post, double salary) {
          super(name, age, post, salary);
      }
  
      @Override
      public String introduce() {
          return super.introduce();
      }
  }
  ```

- `AssProfessor` （副教授类）

  ```java
  package com.homework.Homework3;
  
  public class AssProfessor extends Teacher{
      public AssProfessor(String name, int age, String post, double salary) {
          super(name, age, post, salary);
      }
  
      @Override
      public String introduce() {
          return super.introduce();
      }
  }
  ```

- `Lecturer`  （讲师类）

  ```java
  package com.homework.Homework3;
  
  public class Lecturer extends Teacher{
      public Lecturer(String name, int age, String post, double salary) {
          super(name, age, post, salary);
      }
  
      @Override
      public String introduce() {
          return super.introduce();
      }
  }
  ```

- `TeacherApp` （测试类）

  ```java
  package com.homework.Homework3;
  
  public class TeacherApp {
      public static void main(String[] args) {
          Teacher teacher = new Teacher("tom",20,"正高级",5000);
          Professor professor = new Professor("jack",50,"正高级",13000);
          AssProfessor assProfessor = new AssProfessor("mary",45,"正高级",12000);
          Lecturer lecturer = new Lecturer("macs", 30, "正高级", 12000);
  
          System.out.println(teacher.introduce());
          System.out.println(professor.introduce());
          System.out.println(assProfessor.introduce());
          System.out.println(lecturer.introduce());
  
      }
  }
  ```

  

## 第四题【Employee类 继承】

```
父类：员工类（Employee）
子类：部门经理类、普通员工类
(1)部门经理工资 = 1000+单日工资*天数*等级(1.2)    ==》 奖金 + 基本工资
(2)普通员工工资 = 单日工资*天数*等级(1.0)   ==》 基本工资
(3)员工属性：姓名，单日工资，工作天数
(4)员工方法（打印工资）
(5)普通员工及部门经理都是员工的子类，需要重写打印工资方法
(6)定义并初始化普通员工对象，调用打印工资方法输出方法；定义并初始化部门经理对象，调用打印工资方法输出方法；
```

- `Employee` 员工类

  ```java
  package com.homework.Homework4;
  /*
  * 父类：员工类（Employee）
  * 子类：部门经理类、普通员工类
  * (1)部门经理工资 = 1000+单日工资*天数*等级(1.2)    ==》 奖金 + 基本工资
  * (2)普通员工工资 = 单日工资*天数*等级(1.0)   ==》 基本工资
  * (3)员工属性：姓名，单日工资，工作天数
  * (4)员工方法（打印工资）
  * (5)普通员工及部门经理都是员工的子类，需要重写打印工资方法
  * (6)定义并初始化普通员工对象，调用打印工资方法输出方法；定义并初始化部门经理对象，调用打印工资方法输出方法；
  * */
  public class Employee {
          private String name;
          private double daySalary;
          private double day;
          private double grade;
  
      public Employee(String name, double daySalary, double day, double grade) {
          this.name = name;
          this.daySalary = daySalary;
          this.day = day;
          this.grade = grade;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public double getDaySalary() {
          return daySalary;
      }
  
      public void setDaySalary(double daySalary) {
          this.daySalary = daySalary;
      }
  
      public double getDay() {
          return day;
      }
  
      public void setDay(double day) {
          this.day = day;
      }
  
      public double getGrade() {
          return grade;
      }
  
      public void setGrade(double grade) {
          this.grade = grade;
      }
  
      public double showTotalSalary(){
          return daySalary*day*grade;
      }
  }
  
  ```

- `Manager` 部门经理类

  ```java
  package com.homework.Homework4;
  
  public class Manager extends Employee {
      public Manager(String name, double daySalary, double day, double grade) {
          super(name, daySalary, day, grade);
      }
  
      @Override
      public double showTotalSalary() {
          return 1000 + super.showTotalSalary();
      }
  }
  
  ```

  

- `Worker` 普通员工类

  ```java
  package com.homework.Homework4;
  
  public class Worker extends Employee{
  
      public Worker(String name, double daySalary, double day, double grade) {
          super(name, daySalary, day, grade);
      }
  
      @Override
      public double showTotalSalary() {
          return super.showTotalSalary();
      }
  }
  
  ```

  

- `EmployeeApp` 测试类

  ```java
  package com.homework.Homework4;
  
  public class EmployeeApp {
      public static void main(String[] args) {
          Manager tom = new Manager("tom", 5000, 30, 1.2);
          Worker jack = new Worker("jack", 2000, 30, 1.0);
  
          System.out.println("经理工资：" + tom.showTotalSalary());
          System.out.println("员工工资：" + jack.showTotalSalary());
      }
  }
  ```



## 第五题【Vehicles接口 实现】

```
题目：
1.有一个交通工具类 Vehicles，有 work接口
2.有 Horse 类和 Boat 类分别实现 Vehicles
3.创建交通工具工厂类，有两个方法分别获得交通工具 Horse 和 Boat
4.有 Person 类，有 name 和 Vehicles 属性，在构造器中为两个属性赋值
5.实例化 Person 对象 "唐僧"，要求一般情况下 Horse作为交通工具，遇到大河时用 Boat作为交通工具。
```

- Boat类

  ```java
  package com.stage_homework.houmework5;
  
  public class Boat implements Vehicles{
      @Override
      public void work() {
          System.out.println("使用Boat交通工具.....");
      }
  }
  ```

- Horse 类

  ```java
  package com.stage_homework.houmework5;
  
  public class Horse implements Vehicles{
      @Override
      public void work() {
          System.out.println("使用Horse交通工具....");
      }
  }
  ```

- Person类

  ```java
  package com.stage_homework.houmework5;
  
  public class Person {
      private String name;
      private Vehicles vehicles;
  
      public Person(String name, Vehicles vehicles) {
          this.name = name;
          this.vehicles = new Horse();
      }
  
      //将一个具体的要求封装成一个方法
      public void passRiver() {
          if (!(vehicles instanceof Boat)) {
              vehicles = VehiclesFactory.getBoat();
          }
          vehicles.work();
      }
  
      public void common() {
          //vehicles 为 null 时 vehicles instanceof Horse 为 false
          //vehicles 为 Horse 时  vehicles instanceof Horse 为 false
          //vehicles 为 Boat 时 vehicles instanceof Horse 为 true
          if (!(vehicles instanceof Horse)) {
              vehicles = VehiclesFactory.getHorse();
          }
          vehicles.work();
      }
  
  }
  ```

- Vehicles接口

  ```java
  package com.stage_homework.houmework5;
  
  interface Vehicles {
      public void work();
  }
  ```

- VehiclesFactory类

  ```java
  package com.stage_homework.houmework5;
  
  public class VehiclesFactory {
  
      public static Horse getHorse(){
          return new Horse();
      }
  
      public static Boat getBoat(){
          return new Boat();
      }
  }
  ```

- PersonApp

  ```java
  package com.stage_homework.houmework5;
  
  public class PersonApp {
      public static void main(String[] args) {
          Person ts = new Person("唐僧", new Horse());
          ts.common();
          ts.passRiver();
          ts.common();
          ts.common();
          ts.passRiver();
          ts.common();
          ts.passRiver();
          ts.common();
  
      }
  }
  ```

  

## 第六题【Car类里有  Air(空调)内部类】

```
题目：
有一个 Car 类，有属性temperature(温度)，车内有Air(空调)类，有吹风的功能flow，Air会监视车内的温度，如果温度超过40度则吹冷气，如果温度低于0度则吹暖气，如果温度超过0-40度则关掉空调。实例化具有不同温度的Car对象，调用空调的flow方法，测试空调吹的风是否正确。
```

- 代码

  ```java
  package com.stage_homework.houmework6;
  
  public class CarApp {
      public static void main(String[] args) {
          Car car = new Car(60);
          car.getAir().flow();
          Car car2 = new Car(-1);
          car2.getAir().flow();
          Car car3 = new Car(20);
          car3.getAir().flow();
      }
  }
  
  class Car {
      private double temperature;
  
      public Car(double temperature) {
          this.temperature = temperature;
      }
  
      class Air {
          public void flow() {
              if (temperature > 40) {
                  System.out.println("温度大于40°，空调吹冷气....");
              } else if (temperature < 0) {
                  System.out.println("温度小于0°，空调吹热气....");
              } else {
                  System.out.println("温度正常，空调停止工作....");
              }
          }
      }
      
      //设计一个对外开放的方法，返回内部类Air的对象，不定义一个这样的方法，在main中也可以通过 new Car(70).new Air().flow(); 来实现
      public Air getAir() {
          return new Air();
      }
  }
  
  ```



## 第七题【News类  使用集合 】

```
按要求实现:
(1)封装一个新闻类，包含标题和内容属性，提供get、set方法，toString方法，打印对象时只打印标题;
(2)只提供一个带参数的构造器，实例化对象时，只初始化标题;并且实例化两个对象:
新闻一:新冠确诊病例超千万，数百万印度教信徒赴恒河“圣浴”引民众担忧
新闻二:男子突然想起2个月前钓的鱼还在网兜里，捞起一看赶紧放生
(3)将新闻对象添加到ArrayList集合中，并且进行倒序遍历;
(4)在遍历集合过程中，对新闻标题进行处理，超过15字的只保留前15个，然后在后边加
(5)在控制台打印遍历出经过处理的新闻标题;

```

- 代码

  ```java
  package com.stage_homework.CollectionHomework01;
  
  import java.util.ArrayList;
  import java.util.List;
  
  @SuppressWarnings({"all"})
  public class homework01 {
      public static void main(String[] args) {
          
          ArrayList arrayList = new ArrayList();
          arrayList.add(new News("新冠确诊病例超千万，数百万印度教信徒赴恒河\"圣浴\"引民众担忧"));
          arrayList.add(new News("男子突然想起 2个月前钓的鱼还在网兜里，捞起一看赶紧放生"));
  
          int size = arrayList.size();
  
          for (int i = size - 1; i >= 0; i--) {
              News news = (News) arrayList.get(i);
              System.out.println(processTitle(news.getTitle()));
          }
      }
  
      //截取标题前15位
      public static String processTitle(String title){
  
          if (title == null){
              return "";
          }
  
          if (title.length()>15){
              return title.substring(0,15) + "..."; //[0，15)前闭 后开
          }else {
              return title;
          }
      }
  
  }
  
  @SuppressWarnings({"all"})
  class News {
  
      private String title;
      private String content;
  
      public News(String title) {
          this.title = title;
      }
  
      public String getTitle() {
          return title;
      }
  
      public void setTitle(String title) {
          this.title = title;
      }
  
      public String getContent() {
          return content;
      }
  
      public void setContent(String content) {
          this.content = content;
      }
  
      @Override
      public String toString() {
          return title;
      }
  }
  
  ```



## 第八题 【集合常用方法回顾】

```
对集合的一些常用方法进行复习
```

- 代码

  ```java
  package com.stage_homework.CollectionHomework01;
  
  import java.util.ArrayList;
  import java.util.HashSet;
  
  @SuppressWarnings({"all"})
  public class Homework02 {
      public static void main(String[] args) {
          ArrayList arrayList = new ArrayList();
          HashSet hashSet = new HashSet();
          Car car1 = new Car("宝马", 200000);
          Car car2 = new Car("奔驰", 10000000);
  
         hashSet.add(car1);
         hashSet.add(car2);
  
          //添加单个元素
          arrayList.add(car1);
          arrayList.add(car2);
          System.out.println(arrayList);
          System.out.println("==============");
          //删除指定元素
          arrayList.remove(car1);
          System.out.println(arrayList);
          System.out.println("==============");
          //查找元素是否存在
          System.out.println(arrayList.contains(car1));
          System.out.println(arrayList.contains(car2));
          System.out.println("==============");
          //获取元素个数
          System.out.println("元素个数：" + arrayList.size());
          System.out.println("==============");
          //判空
          System.out.println(arrayList.isEmpty());
          System.out.println("==============");
          //清空
          arrayList.clear();
          System.out.println(arrayList);
          System.out.println("==============");
          //添加对个元素
          arrayList.addAll(hashSet);
          System.out.println(arrayList);
          System.out.println("=============");
          //查找多个元素
          System.out.println(arrayList.containsAll(hashSet));
          System.out.println("=============");
          //删除多个元素
          arrayList.removeAll(hashSet);
          System.out.println(arrayList);
  
      }
  }
  
  class Car {
  
      private String name;
      private double price;
  
      public Car(String name, double price) {
          this.name = name;
          this.price = price;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public double getPrice() {
          return price;
      }
  
      public void setPrice(double price) {
          this.price = price;
      }
  
      @Override
      public String toString() {
          return "Car{" +
                  "name='" + name + '\'' +
                  ", price=" + price +
                  '}';
      }
  }
  ```



## 第九题【HashMap】

```
按要求完成下列任务:
(1)使用 HashMap 类实例化一个Map类型的对象m，键(String) 和值(int) 分别用于存储员工的姓名和工资，存入数据如下：jack--650元； tom--1200元；smith---2900元；
(2)将jack的工资更改为2600元
(3)为所有员工工资加薪100元
(4)遍历集合中所有的员工
(5)遍历集合中所有

```

- 代码

  ```java
  package com.stage_homework.CollectionHomework01;
  
  
  import java.util.HashMap;
  import java.util.Iterator;
  import java.util.Map;
  import java.util.Set;
  
  @SuppressWarnings({"all"})
  public class Homework03 {
      public static void main(String[] args) {
  
  
          HashMap hashMap = new HashMap();
          hashMap.put("jack", 650);
          hashMap.put("tom", 1200);
          hashMap.put("smith", 2900);
          System.out.println(hashMap);
  
          hashMap.put("jack", 2600);
          System.out.println(hashMap);
  
          //为所有员工工资加薪 100元
          Set keySet = hashMap.keySet(); //取出键
          for (Object key : keySet) {
              hashMap.put(key, (Integer) hashMap.get(key) + 100);
          }
          System.out.println(hashMap);
  
  
          //迭代器遍历
          Set entrySet = hashMap.entrySet();
          Iterator iterator = entrySet.iterator();
          while (iterator.hasNext()) {
              Map.Entry entry = (Map.Entry) iterator.next();
              System.out.println(entry.getKey() + "----" + entry.getValue());
          }
  
          //遍历员工
          for (Object o : hashMap.entrySet()) {
              System.out.println(o);
          }
          //遍历工资
          for (Object value : hashMap.values()) {
              System.out.println(value);
          }
  
  
      }
  }
  
  ```

  

## 第十题【HashSet和TreeSet  去重】

- 试分析HashSet和TreeSet分别如何实现去重

  ```
  (1)HashSet的去重机制：hashCode() + equals()，底层先通过存入对象，进行运算得到一个hash值，通过hash值得到对应的索引，如果发现table索引所在位置，没有数据，就直接存放，如果有数据，就进行equals比较【遍历比较】，如果比较后，不相同，就加入，否则就不加入 。
  (2)TreeSet的去重机制：如果你传入了一个Comnparator匿名对象，就是用实现的Comnpare去重，如果方法返回0，就认为是相同的元素/数据，就不添加，rg你没有传入一个Comparator匿名对象实现的Compareable接口的conpareTo去重。
  
  ```



## 第十一题【集合 + 定制排序】

```
题目要求：
(1)员工 Emoloyee类，该类包含:private成员变量name,sal,birthday,其中 birthday 为 MyDate类的对象;
(2)为每一个属性定义getter, setter方法;
(3)重写toString方法输出name, sal, birthday
(4) MyDate类包含:private成员变量month,day,year;并为每一个属性定义getter,setter方法;
(5)创建该类的3个对象,并把这些对象放入ArrayList 集合中(ArrayList需使用泛型来定义)，对集合中的元素进行排序,并遍历输出:
	排序方式:调用ArrayList 的sort方法，传入Comparator对象[使用泛型],先按照name排序,如果name相同，则按生日日期的先后排序。【即:定制排序】

```

- GenericHomework01.java

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

- Employee.java

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

- MyDate.java

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



## 第十二题 【泛型 + JUnit单元测试】

```
定义个泛型类 DAO<T>，在其中定义一个 Map 成员变量，Map 的键为 String 类型，值为 T 类型
分别创建以下方法:
(1) public void save(String id,T entity): 保存T类型的对象到 Map 成员变量中
(2) public T get(String id): 从 map 中获取 id 对应的对象
(3) public void update(String id,T entity):替换 map 中 key 为 id 的内容,改为entity 对象
(4) public List<T> list(): 返回 map 中存放的所有 T 对象
(5) public void delete(String id): 删除指定 id 对象
定义一个 User类:
该类包含: private 成员变量(int类型) id,age; (String类型)name.

创建 DAO类的对象，分别调用其 save、get、update、list、delete方法来操作 User 对象，使用 Junit单元测试类进行测试。

```

- GenericHomework.java

  ```java
  package com.stage_homework.generichomework;
  
  import org.junit.jupiter.api.Test;
  import java.util.List;
  
  public class GenericHomework {
      public static void main(String[] args) {
  
      }
  
      @Test  //JUnit 单元测试
      public void testList() {
          DAO<User> userDAO = new DAO<>();
          userDAO.save("001", new User(1, 20, "tom"));
          userDAO.save("002", new User(2, 25, "jack"));
          userDAO.save("003", new User(3, 23, "mary"));
  
          List<User> list = userDAO.list();
          System.out.println("list=" + list);
      }
  }
  
  ```

- DAO.java

  ```java
  package com.stage_homework.generichomework;
  
  import java.util.*;
  
  public class DAO<T> {private Map<String, T> map = new HashMap<>();
   	//保存T类型的对象到 Map 成员变量中
      public void save(String id, T entity) {
          map.put(id, entity);
      }
  	//从 map 中获取 id 对应的对象
      public T get(String id) {
          return map.get(id);
      }
  	//替换 map 中 key 为 id 的内容,改为 entity 对象
      public void update(String id, T entity) {
          map.put(id, entity);
      }
  
      // 返回 map 中存放的所有 T 对象
      public List<T> list() {
          //创建ArrayList
          List<T> list = new ArrayList();
          //遍历map
          Set<String> keySet = map.keySet();
          for (String key : keySet) {
              list.add(get(key));
          }
          return list;
      }
  	//删除指定 id 对象
      public void delete(String id) {
          map.remove(id);
      }
  
  }
  
  ```

- User.java

  ```java
  package com.stage_homework.generichomework;
  
  public class User {
  
      private int id;
      private int age;
      private String name;
  
      public User(int id, int age, String name) {
          this.id = id;
          this.age = age;
          this.name = name;
      }
  
      public int getId() {
          return id;
      }
  
      public void setId(int id) {
          this.id = id;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      @Override
      public String toString() {
          return "User{" +
                  "id=" + id +
                  ", age=" + age +
                  ", name='" + name + '\'' +
                  '}';
      }
  }
  
  ```



## 第十三题【异常处理 + 用户登录】

```
题目:
	输入用户名、密码、邮箱，如果信息录入正确，则提示注册成功，否则生成异常对象
要求：
    (1)用户名长度 2 或 3 或 4
    (2)密码的长度为 6，要求全是数字 isDigital
    (3)邮箱中包含 @ 和 .   并且 @ 在 . 前面

```

- LoginUser.java

  ```java
  package com.stage_homework.loginuser;
  
  /**
   * 题目:
   * 输入用户名、密码、邮箱，如果信息录入正确，则提示注册成功，否则生成异常对象
   * 要求：
   * (1)用户名长度 2 或 3 或 4
   * (2)密码的长度为 6，要求全是数字 isDigital
   * (3)邮箱中包含 @ 和 .   并且 @ 在 . 前面
   */
  public class LoginUser {
      public static void main(String[] args) {
              String name = "tom";
              String pwd = "123123";
              String email = "111@sdsd.com";
          try {
              userRegister(name,pwd,email);
              System.out.println("注册成功！");
          } catch (Exception e) {
              System.out.println("异常信息： " + e.getMessage());
          }
      }
  
      public static void userRegister(String name, String pwd, String email) {
  
  
          int username = name.length();
          if (!(username >= 2 && username <= 4)) {
              throw new RuntimeException("用户名长度为2或3或4");
          }
          int userpwd = pwd.length();
          if (!(userpwd == 6 && isDigital(pwd))) {
              throw new RuntimeException("密码的长度为 6，要求全是数字 isDigital");
          }
  
          int i = email.indexOf('@');
          int j = email.indexOf('.');
          if (!(i > 0 && j > i)) {
              throw new RuntimeException("邮箱中包含@和. 并且@在.前面");
          }
  
      }
  
      public static boolean isDigital(String pwd) {
          char[] chars = pwd.toCharArray();
          for (char ch : chars) {  //这里只需要遍历，使用foreach方便一点
              if (ch < '0' || ch > '9') {
                  return false;
              }
          }
          return true;
      }
  }
  
  
  ```

## 第十四题【IO + 创建文件 + 写入】

```
题目：
    (1) 在判断 d 盘下是否有文件夹 mytemp ,如果没有就创建 mytemp
    (2)在 D:\\mytemp 目录下，创建 hello.txt
    (3) 如果 hello.txt  已经存在，提示该文件已经存在，就不再重复创建了
    (4) 并且 hello.txt 文件中 ，导入 hello，world！
```

```java
package com.stage_homework.io.iohomework01;

import java.io.*;

public class HomeWork01 {
    public static void main(String[] args) {
        test01();
    }

    public static void test01() {
        String dirName = "D:\\mytemp";
        File dir = new File(dirName);

        if (dir.exists()) {
            System.out.println("此目录已存在！！");
        } else {
            dir.mkdir();
        }

        String fileName = "D:\\mytemp\\hello.txt";
        File file = new File(fileName);
        try {
            if (file.exists()){
                System.out.println("该文件已存在！！！");
            }else{
                file.createNewFile();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        FileWriter fileWriter = null;
        try {
            fileWriter = new FileWriter(fileName);
            String str = "hello,world!";
            fileWriter.write(str);
            System.out.println("写入成功！！");
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileWriter.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

```







