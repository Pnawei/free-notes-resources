---
title: java小项目
date: 2021-12-01
tags: 
    - qq通信
    - 零钱通	
    - Java
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。 

两个阶段项目： 一是零钱通   二是多用户即时通信系统  

<!-- more -->

## 1  零钱通项目（类似微信零钱通）

1、项目需求说明

2、 使用 java 开发零钱同项目，可以完成收益入账、消费、查看明细，退出系统等功能

3、输出界面显示![image-20211117203927939](https://i.loli.net/2021/11/17/xhKG9SZeurOwRaN.png)

### 第一种方法（面向过程）

```java
//下面代码使用的简单的一种字符串拼接实现
package com.SmallChange;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

public class SmallChangeSys {
    /*
     * 1 化繁为简
     * 2 完成零钱通明细
     * 3 收益入账
     * 4 消费
     * 5 退出
     * 6 退出判断，如果要退出，给出提示"你确定要退出吗？y/n" ,必须输入正确的y/n，否则一直执行循环，直到输入正确的y/n
     * 7 在收益入账和消费时，判断金额是否合理，并给出相应提示
     * */
    public static void main(String[] args) {
        //定义相关变量
        boolean loop = true;
        Scanner scanner = new Scanner(System.in);
        String key = "";

        //2 完成零钱通明细
        //3种思路 (1) 可以把收益入账和消费，保存到数组  (2) 可以使用对象  (3) 简单的话可以使用String拼接 
        String detiles = "-----------------零钱通明细---------------------";

        //3 收益入账
        double money = 0;
        double balance = 0;
        Date date = null; //表示日期
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm");  //可以用于日期的格式化

        //4 消费
        String note = ""; //消费说明

        //6 退出判断
        String choice = "";

        do {
            System.out.println("\n===========零钱通菜单=============");
            System.out.println("\t\t\t1 零钱通明细");
            System.out.println("\t\t\t2 收益入账");
            System.out.println("\t\t\t3 消 费");
            System.out.println("\t\t\t4 退 出");
            System.out.println("================================");

            System.out.println("请选择(1-4): ");
            key = scanner.next();

            switch (key) {
                case "1":
                    System.out.println(detiles);
                    break;
                case "2":
                    System.out.println("收益入账金额：");
                    money = scanner.nextDouble();
                    //money 的值范围应该校验
                    if (money <= 0) {
                        System.out.println("收益入账金额需要 大于 0");
                        break;
                    }
                    balance += money;
                    //拼接到收益入账信息中去
                    date = new Date(); //获取当前的时间
                    detiles += "\n收益入账\t+" + money + "\t" + sdf.format(date) + "\t" + "余额：" + balance;
                    break;
                case "3":
                    System.out.println("消费金额：");
                    money = scanner.nextDouble();
                    //money 的值范围应该校验
                    if (money <= 0 || money > balance) {
                        System.out.println("您的消费金额应该在 0-" + balance + " 之间");
                        break;
                    }
                    System.out.println("消费说明：");
                    note = scanner.next();
                    balance -= money;
                    //拼接到收益入账信息中去
                    date = new Date();
                    detiles += "\n" + note + "\t-" + money + "\t" + sdf.format(date) + "\t" + "余额：" + balance;
                    break;
                case "4":
                    /*
                     * 这里使用功能拆分，每一块代码实现一个小功能
                     * */
                    while (true) {//这个功能：要求用户必须输入y/n,否则循环继续执行
                        System.out.println("你确定要退出吗？y/n");
                        choice = scanner.next();
                        if ("y".equals(choice) || "n".equals(choice)) {
                            break;
                        }
                    }
                    //分功能2，把判断语句独立到 while 之外，有利于扩展
                    if ("y".equals(choice)) {
                        loop = false;
                    }
                    break;
                default:
                    System.out.println("选择有误，请重新选择");
            }
        } while (loop);

        System.out.println("---------退出了零钱通项目---------");
    }
}

```



### 第二种方法（面向对象）

- `SmallChangeSysOOP` 函数类

  ```java
  package com.SmallChange11;
  
  import java.text.SimpleDateFormat;
  import java.util.Date;
  import java.util.Scanner;
  
  /*
   * 该类是实现零钱通各个功能的类
   * 使用OOP（面向对象进行编程）
   * 2 完成零钱通明细
   * 3 收益入账
   * 4 消费
   * 5 退出
   * 6 退出判断，如果要退出，给出提示"你确定要退出吗？y/n" ,必须输入正确的y/n，否则一直执行循环，直到输入正确的y/n
   * 7 在收益入账和消费时，判断金额是否合理，并给出相应提示
   * */
  public class SmallChangeSysOOP {
      //属性
      //定义相关变量
      boolean loop = true;
      Scanner scanner = new Scanner(System.in);
      String key = "";
  
      //2 完成零钱通明细
      //3种思路 (1) 可以把收益入账和消费，保存到数组 (2) 可以使用对象  (3) 简单的话可以使用String拼接
      String details = "-----------------零钱通明细---------------------";
  
      //3 收益入账
      double money = 0;
      double balance = 0;
      Date date = null; //表示日期
      SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm");  //可以用于日期的格式化
  
      //4 消费
      String note = ""; //消费说明
  
      //6 退出判断
      String choice = "";
  
  
      //显示出菜单的方法
      public void mainMenu() {
          do {
              System.out.println("\n==============零钱通菜单(OOP)===============");
              System.out.println("\t\t\t1  零钱通明细");
              System.out.println("\t\t\t2  收益入账");
              System.out.println("\t\t\t3  消 费");
              System.out.println("\t\t\t4  退 出");
              System.out.println("======================================");
  
              System.out.println("请选择(1-4): ");
              key = scanner.next();
  
              switch (key) {
                  case "1":
                      this.detials();
                      break;
                  case "2":
                      this.income();
                      break;
                  case "3":
                      this.pay();
                      break;
                  case "4":
                      this.exit();
                      break;
                  default:
                      System.out.println("选择有误，请重新选择");
              }
          } while (loop);
  
          System.out.println("---------退出了零钱通项目---------");
      }
  
      //实现零钱通的明细
      public void detials() {
          System.out.println(details);
      }
  
      //实现收益入账
      public void income() {
          System.out.println("收益入账金额：");
          money = scanner.nextDouble();
          //money 的值范围应该校验
          if (money <= 0) {
              System.out.println("收益入账金额需要 大于 0");
              return;//退出方法，不在执行后面的代码
          }
          balance += money;
          //拼接到收益入账信息中去
          date = new Date(); //获取当前的时间
          details += "\n收益入账\t+" + money + "\t" + sdf.format(date) + "\t" + "余额：" + balance;
      }
  
      //消费
      public void pay() {
          System.out.println("消费金额：");
          money = scanner.nextDouble();
          //money 的值范围应该校验
          if (money <= 0 || money > balance) {
              System.out.println("您的消费金额应该在 0-" + balance + " 之间");
              return;
          }
          System.out.println("消费说明：");
          note = scanner.next();
          balance -= money;
          //拼接到收益入账信息中去
          date = new Date();
          details += "\n" + note + "\t-" + money + "\t" + sdf.format(date) + "\t" + "余额：" + balance;
      }
  
  
      //退出   退出判断，如果要退出，给出提示"你确定要退出吗？y/n" ,必须输入正确的y/n，否则一直执行循环，直到输入正确的y/n
      public void exit() {
          /*
           * 这里使用功能拆分，每一块代码实现一个小功能
           * */
          while (true) {//这个功能：要求用户必须输入y/n,否则循环继续执行
              System.out.println("你确定要退出吗？y/n");
              choice = scanner.next();
              if ("y".equals(choice) || "n".equals(choice)) {
                  break;
              }
          }
          //分功能2，把判断语句独立到 while 之外，有利于扩展
          if ("y".equals(choice)) {
              loop = false;
          }
      }
  
  }
  
  ```

  

- `SmallChangeSysApp` 实现类

  ```java
  package com.SmallChange11;
  /*
  * 这里我们直接调用 SmallChangeSysOOP 对象，显示显示主菜单即可
  * */
  public class SmallChangeSysApp {
      public static void main(String[] args) {
  
          new SmallChangeSysOOP().mainMenu();
      }
  }
  
  ```



## 2 房屋出租系统

### 项目设计-程序框架图

![image-20211120161130219](https://i.loli.net/2021/11/20/jWt9U5S7KIxhkRA.png)

- 实现基于文本界面的《房屋出租软件》

- 能够实现对房屋信息的添加、修改、删除（用数组实现），并能够打印房屋出租明细表。

- 思维导图

![image-20211120153527970](https://i.loli.net/2021/11/20/cnDLC9SZm8XA5dR.png)



- 实现类（`HouseRentApp`类）

  ```java
  package com.houserent;
  
  import com.houserent.view.HouseView;
  
  public class HouseRentApp {
      public static void main(String[] args) {
          //创建HouseView 对象，并且显示主菜单，是程序的入口
          new HouseView().mainMenu();
      }
  }
  ```

- `domain` 包下的 `House`类

  ```java
  package com.houserent.domain;
  
  /**
   * House的对象表示一个房屋信息
   */
  public class House {
      //编号  房主  电话  地址  月租 状态(未出租/已出租)
      private int id;
      private String name;
      private String phone;
      private String address;
      private int rent;
      private String state;
  
      public House(int id, String name, String phone, String address, int rent, String state) {
          this.id = id;
          this.name = name;
          this.phone = phone;
          this.address = address;
          this.rent = rent;
          this.state = state;
      }
  
  
      public int getId() {
          return id;
      }
  
      public void setId(int id) {
          this.id = id;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public String getPhone() {
          return phone;
      }
  
      public void setPhone(String phone) {
          this.phone = phone;
      }
  
      public String getAddress() {
          return address;
      }
  
      public void setAddress(String address) {
          this.address = address;
      }
  
      public String getState() {
          return state;
      }
  
      public void setState(String state) {
          this.state = state;
      }
  
      public int getRent() {
          return rent;
      }
  
      public void setRent(int rent) {
          this.rent = rent;
      }
  
      //编号  房主  电话  地址  月租 状态(未出租/已出租)
      @Override
      public String toString() {
          return id +
                  "\t\t" + name +
                  "\t" + phone +
                  "\t\t" + address +
                  "\t" + rent +
                  "\t\t" + state;
      }
  }
  ```

- `service` 包下的 `HouseService`类 （业务实现类）

  ```java
  package com.houserent.service;
  
  import com.houserent.domain.House;
  
  /**
   * HouseService.java => 类【业务层】
   * 定义 House[] ,保存 House 对象
   * 1 响应 HouseView 的调用
   * 2 完成对房屋信息的各种操作 ( 增删改查 c[create] r[read] u[update] d[delete])
   */
  public class HouseService {
      private House[] houses; //保存 House对象
      private int houseNums = 1; //记录当前有多少个房屋信息
      private int idCounter; //记录当前的id增长到哪个值
  
      //构造器
      public HouseService(int size){
          //new houses
          houses = new House[size]; //当创建HouseService对象，指定数组大小
          //为了配合测试，这里初始化一个House 对象
          houses[0] = new House(1,"tom","110","九江共青",2000,"未出租");
  
      }
  
      //findById 方法，返回House对象或者null
      public House findById(int findId){
          for (int i = 0; i < houseNums; i++) {
              if (findId == houses[i].getId()){
                  return houses[i];
              }
          }
          return null;
      }
  
  
      //del 方法，删除一个房屋信息
      public boolean del(int delId) {
          
          //应当先找到要删除的房屋信息对应的下标
          //注意：下标和房屋的编号不是一回事
          int index = -1;
          for (int i = 0; i < houseNums; i++) {
              if (delId == houses[i].getId()){//要删除的房屋(id),是数组下标为i的元素
                  index = i; //使用index记录i
              }
          }
          if (index == -1){//说明delId再数组中不存在
              return false;
          }
          for (int i = index; i < houseNums - 1; i++) {
              houses[i] = houses[i+1];
          }
  //        houses[houseNums - 1] = null;
  //        houseNums--;
          houses[--houseNums] = null; //把当前存在房屋信息的最后一个，设置为null
          return true;
      }
  
  
      //添加add对象，返回boolean
      public boolean add(House newHouse){
  
          //判断我们是否还可以继续添加(暂时不考虑数组扩容的问题)
          if (houseNums == houses.length){//不能添加
             System.out.println("数组已满，不能再添加了.....");
             return false;
          }
          //把newHouse对象加入到
          houses[houseNums++] = newHouse;
          idCounter++;
          newHouse.setId(++idCounter);
          return true;
      }
  
      //list 方法，返回一个数组
      public House[] list(){
          return houses;
      }
  }
  ```

- `utils` 包下的 `Utility`类  

  ```java
  package com.houserent.utils;
  
  /**
   工具类的作用:
   处理各种情况的用户输入，并且能够按照程序员的需求，得到用户的控制台输入。
   */
  import java.util.*;
  
  public class Utility {
      //静态属性。。。
      private static final Scanner scanner = new Scanner(System.in);
  
  
      /**
       * 功能：读取键盘输入的一个菜单选项，值：1——5的范围
       * @return 1——5
       */
      public static char readMenuSelection() {
          char c;
          for (; ; ) {
              String str = readKeyBoard(1, false);//包含一个字符的字符串
              c = str.charAt(0);//将字符串转换成字符char类型
              if (c != '1' && c != '2' &&
                      c != '3' && c != '4' && c != '5') {
                  System.out.print("选择错误，请重新输入：");
              } else break;
          }
          return c;
      }
  
      /**
       * 功能：读取键盘输入的一个字符
       * @return 一个字符
       */
      public static char readChar() {
          String str = readKeyBoard(1, false);//就是一个字符
          return str.charAt(0);
      }
      /**
       * 功能：读取键盘输入的一个字符，如果直接按回车，则返回指定的默认值；否则返回输入的那个字符
       * @param defaultValue 指定的默认值
       * @return 默认值或输入的字符
       */
  
      public static char readChar(char defaultValue) {
          String str = readKeyBoard(1, true);//要么是空字符串，要么是一个字符
          return (str.length() == 0) ? defaultValue : str.charAt(0);
      }
  
      /**
       * 功能：读取键盘输入的整型，长度小于2位
       * @return 整数
       */
      public static int readInt() {
          int n;
          for (; ; ) {
              String str = readKeyBoard(10, false);//一个整数，长度<=10位
              try {
                  n = Integer.parseInt(str);//将字符串转换成整数
                  break;
              } catch (NumberFormatException e) {
                  System.out.print("数字输入错误，请重新输入：");
              }
          }
          return n;
      }
      /**
       * 功能：读取键盘输入的 整数或默认值，如果直接回车，则返回默认值，否则返回输入的整数
       * @param defaultValue 指定的默认值
       * @return 整数或默认值
       */
      public static int readInt(int defaultValue) {
          int n;
          for (; ; ) {
              String str = readKeyBoard(10, true);
              if (str.equals("")) {
                  return defaultValue;
              }
  
              //异常处理...
              try {
                  n = Integer.parseInt(str);
                  break;
              } catch (NumberFormatException e) {
                  System.out.print("数字输入错误，请重新输入：");
              }
          }
          return n;
      }
  
      /**
       * 功能：读取键盘输入的指定长度的字符串
       * @param limit 限制的长度
       * @return 指定长度的字符串
       */
  
      public static String readString(int limit) {
          return readKeyBoard(limit, false);
      }
  
      /**
       * 功能：读取键盘输入的指定长度的字符串或默认值，如果直接回车，返回默认值，否则返回字符串
       * @param limit 限制的长度
       * @param defaultValue 指定的默认值
       * @return 指定长度的字符串
       */
  
      public static String readString(int limit, String defaultValue) {
          String str = readKeyBoard(limit, true);
          return str.equals("")? defaultValue : str;
      }
  
  
      /**
       * 功能：读取键盘输入的确认选项，Y或N
       * 将小的功能，封装到一个方法中.
       * @return Y或 N
       */
      public static char readConfirmSelection() {
          System.out.println("请输入你的选择(Y/N): 请小心选择");
          char c;
          for (; ; ) {//无限循环
              //在这里，将接受到字符，转成了大写字母
              //y => Y n=>N
              String str = readKeyBoard(1, false).toUpperCase();
              c = str.charAt(0);
              if (c == 'Y' || c == 'N') {
                  break;
              } else {
                  System.out.print("选择错误，请重新输入：");
              }
          }
          return c;
      }
  
      /**
       * 功能： 读取一个字符串
       * @param limit 读取的长度
       * @param blankReturn 如果为true ,表示 可以读空字符串。
       * 					  如果为false表示 不能读空字符串。
       *
       *	如果输入为空，或者输入大于 limit的长度，就会提示重新输入。
       * @return
       */
      private static String readKeyBoard(int limit, boolean blankReturn) {
  
          //定义了字符串
          String line = "";
  
          //scanner.hasNextLine() 判断有没有下一行
          while (scanner.hasNextLine()) {
              line = scanner.nextLine();//读取这一行
  
              //如果line.length=0, 即用户没有输入任何内容，直接回车
              if (line.length() == 0) {
                  if (blankReturn) return line;//如果blankReturn=true,可以返回空串
                  else continue; //如果blankReturn=false,不接受空串，必须输入内容
              }
  
              //如果用户输入的内容大于了 limit，就提示重写输入
              //如果用户如的内容 >0 <= limit ,我就接受
              if (line.length() < 1 || line.length() > limit) {
                  System.out.print("输入长度（不能大于" + limit + "）错误，请重新输入：");
                  continue;
              }
              break;
          }
  
          return line;
      }
  }
  ```

- `view` 包下的 `HouseView`类  

  ```java
  package com.houserent.view;
  
  import com.houserent.domain.House;
  import com.houserent.service.HouseService;
  import com.houserent.utils.Utility;
  
  /**
   * 1 显示界面
   * 2 接受用户的输入
   * 3 调用 HouseService 完成对房屋信息的操作
   * */
  public class HouseView {
      //所需要的属性
      boolean loop = true;
      char key = ' ';
      HouseService houseService = new HouseService(10); //放10个
  
  
      //根据id修改房屋信息 updateHouse() 方法
      public void updateHouse(){
          System.out.println("-----------------修改房屋信息-----------------");
          System.out.println("请选择待修改房屋的编号(-1表示退出): ");
          int updateId = Utility.readInt();
          if (updateId == -1){
              System.out.println("----------放弃修改房屋信息-------------------");
              return;
          }
          //根据输入的 updateId，查找对象
          //提示：返回的是引用类型【即：就是数组的元素】
          //因此在后面对 house.setXxx(),就会修改HouseService中的数组的元素！！！
          House house = houseService.findById(updateId);
          if (house == null){
              System.out.println("----------你输入的房屋编号不存在-----------");
              return;
          }
          System.out.println("姓名(" + house.getName() + "): ");
          String name = Utility.readString(8,""); //这里用户直接回车表示不修改信息，默认""
          if (!"".equals(name)){
              house.setName(name);
          }
          System.out.println("电话(" + house.getPhone() + "):");
          String phone = Utility.readString(12,"");
          if (!"".equals(phone)){
              house.setPhone(phone);
          }
          System.out.println("地址(" + house.getAddress() + "):");
          String address = Utility.readString(16,"");
          if (!"".equals(address)){
              house.setAddress(address);
          }
          System.out.println("月租(" + house.getRent() + "):");
          int rent = Utility.readInt(-1);
          if (rent != -1){
              house.setRent(rent);
          }
          System.out.println("状态(" + house.getState() + "):");
          String state = Utility.readString(3,"");
          if (!"".equals(state)){
              house.setState(state);
          }
          System.out.println("--------修改房屋信息成功---------------");
  
      }
  
      //编写findHouse() 方法，调用Service 的find 方法
      public void findHouse(){
          System.out.println("------------------查找房屋------------------");
          System.out.println("请选择你要查找的房屋编号: ");
          int findId = Utility.readInt();
          House house = houseService.findById(findId);
          if (house != null){
              System.out.println(house);
          }else{
              System.out.println("-----------------没有该房屋------------------");
          }
      }
  
      //完成退出确认
      public void exit(){
          char c = Utility.readConfirmSelection();
          if (c == 'Y'){
              loop = false;
          }
      }
  
      //编写delHouse() 方法，接收输入的id，调用Service 的del 方法
      public void delHouse(){
          System.out.println("------------------删除房屋信息------------------");
          System.out.println("请选择待删除房屋的编号(-1表示退出): ");
          int delId = Utility.readInt();
          if (delId == -1){
              System.out.println("----------放弃删除房屋信息-------------------");
              return;
          }
          char choice = Utility.readConfirmSelection();
          if (choice == 'Y'){
              if (houseService.del(delId)){ //如果存在可删除的房屋就是true
                  System.out.println("---------删除房屋信息成功---------------");
              }else{
                  System.out.println("---------房屋编号不存在，删除失败------------");
              }
          }else{
              System.out.println("---------------放弃删除房屋信息------------");
          }
      }
  
      //编写addHouse() 接收输入，创建House对象，调用add方法
      public void addHouse(){
          System.out.println("-------------------添加房屋-----------------");
          System.out.println("姓名：");
          String name = Utility.readString(8);
          System.out.println("电话：");
          String phone = Utility.readString(12);
          System.out.println("地址：");
          String address = Utility.readString(16);
          System.out.println("月租：");
          int rent = Utility.readInt();
          System.out.println("状态：");
          String state = Utility.readString(3);
          //创建一个新的House对象，注意 id 是自动分配
          House newhouse = new House(0, name, phone, address, rent, state);
          if (houseService.add(newhouse)){
              System.out.println("===========添加房屋成功===========");
          }else{
              System.out.println("============添加房屋失败===========");
          }
      }
  
      //编写listHouse()方法，显示房屋信息
      public void listHouse(){
          System.out.println("----------------------房屋列表------------------------");
          System.out.println("编号\t\t房主\t\t电话\t\t地址\t\t月租\t\t状态(未出租/已出租)");
          House[] houses = houseService.list();
          for (int i = 0; i < houses.length; i++) {
              if (houses[i] == null){
                  break;
              }
              System.out.println(houses[i]);
          }
      }
  
      //显示主菜单
      public void mainMenu(){
         do {
             System.out.println("\n==============房屋出租系统===============");
             System.out.println("\t\t\t1  新 增 房 源");
             System.out.println("\t\t\t2  查 找 房 屋");
             System.out.println("\t\t\t3  删 除 房 屋");
             System.out.println("\t\t\t4  修 改 房 屋 信 息");
             System.out.println("\t\t\t5  房 屋 列 表");
             System.out.println("\t\t\t6  退  出");
             System.out.println("=========================================");
  
             System.out.println("请选择(1-6): ");
             key = Utility.readChar();
             switch (key){
                 case '1':
                     addHouse();
                     break;
                 case '2':
                     findHouse();
                     break;
                 case '3':
                     delHouse();
                     break;
                 case '4':
                     updateHouse();
                     break;
                 case '5':
                     listHouse();
                     break;
                 case '6':
                     exit();
                     break;
             }
         }while (loop);
         System.out.println("-----------退出了房屋出租系统-------------");
      }
  }
  ```

  



## 3 多用户即时通信系统

### 项目设计-程序框架图

<img src="https://s2.loli.net/2021/12/08/H3EDrlQzNhqbUoJ.png" alt="image.png"  />



