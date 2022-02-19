---
title: json和ajax和i18n
date: 2022-01-04 
tags:
    - json
    - ajax
    - i18n
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

# JSON

## 什么是 JSON？

> JSON（JavaScript Object Notation）是一种轻量级的数据交换格式，易于人阅读和编写。同时也易于机器解析和生成。
>
> JSON采用完全独立于语言的文本格式，而且很多语言都提供了对 json 的支持（包括C，C++，C#，Java，JavaScript，Perl，Python等）。这样就使得 JSON 成为理想的数据交换格式。

**轻量级：** 指的是跟 xml 作比较。

**数据交换：** 指的是客户端和服务器之间业务数据的传递格式。



### JSON 在 JavaScript 中的使用

#### 1、json  的定义

json 是由键值对组成，并且有花括号（大括号）包围。每个键由引号引起来，键和值之间使用冒号进行分割，多组键值对之间用逗号进行分割。

```json
var jsonObj = {
    "key1":12,
    "key2":"abc",
    "key3":true,
    "key4":[11,"arr",false],
    "key5":{
        "key5_1":551,
        "key5_2":"key5_2_value"
    },
    "key6":[{
        "key6_1_1":6611,
        "key6_1_2":"key6_1_2_value"
    },{
        "key6_2_1":6621,
        "key6_2_2":"key6_2_2_value"
    }]
}
```

#### 2、json 的访问

json 本身是一个对象。

json 中的 key 我们可以理解为是对象的一个属性。

json 中的 key 访问就跟访问对象的属性一样：json 对象.key

#### 3、josn 的两个常用方法

json 的存在有两种形式。

一种是：对象的形式存在。我们叫它 json 对象。使用 `JSON.stringify()`

一种是：字符串的形式讯在。我们叫它 json 字符串。使用 `JSON.parse()`

```json
// 把 json 对象转换成为 json 字符串
// 特别像 Java 中对象的 toString
var jsonObjectString = JSON.stringify(jsonObj); 
    
// 把 json 字符串转换成为 json 对象
var josnObj2 = JSON.parse(jsonObjectString);
```

#### 4、JSON 在 java 中的使用

##### javaBean 和 json 的互转

```java
@Test
public void test1(){
    Person person = new Person(1,"哈哈哈");
    //创建 Gosn 对象实例
    Gson gson = new Gson();
    String personJsonString = gson.toJson(person);
    System.out.println(personJsonString);

    //fromJson 把 json 字符串转换回 Java对象
    // 第一个参数是 json 字符串
    // 第二个参数是转换回去的 Java 对象类型
    Person person1 = gson.fromJson(personJsonString, Person.class);
    System.out.println(person1);
}
```

##### List 和 json 的互转

```java
@Test
public void test2(){
    List<Person> personList = new ArrayList<>();
    personList.add(new Person(1,"小李"));
    personList.add(new Person(2,"小王"));

    Gson gson = new Gson();

    String personListJsonString = gson.toJson(personList);
    System.out.println(personListJsonString);

    //使用匿名内部类
    List<Person> list = gson.fromJson(personListJsonString, new TypeToken<ArrayList<Person>>(){}.getType()); 	
    System.out.println(list);
    Person person = list.get(0);
    System.out.println(person);
}
```

##### map 和 json 的互转

```java
@Test
public void test3(){
    Map<Integer,Person> personMap = new HashMap<>();

    personMap.put(1,new Person(1,"Tom"));
    personMap.put(2,new Person(2,"Mary"));

    Gson gson = new Gson();
    String personMapJsonString = gson.toJson(personMap);
    System.out.println(personMapJsonString);

    Map<String,Person> personMap1 = gson.fromJson(personListJsonString,new TypeToken<HashMap<String,Person>>(){}.getType());
    System.out.println(personMap1);
    Person person = personMap1.get(1);
    System.out.println(person);
}
```



# AJAX 请求

## 什么是 AJAX 请求？

> AJAX 即”Asynchronous Javasript And XML“（异步 JaaScript 和 XML），是指一种创建交互式网页应用的网页开发技术。
>
> **ajax 是一种浏览器通过 js 异步发起请求。局部更新页面的技术。**

**jQuery API 中文文档：**https://jquery.cuishifeng.cn/

## 原生 AJAX 请求的实例

```javascript
function ajaxRequest() {
    //1、我们首先要创建 XMLHttpRequest
    var xmlHttpRequest = new XMLHttpRequest();
    //2、调用open方法设置请求参数
    xmlHttpRequest.open("GET","http://localhost:8080/java_web02_war_exploded/ajaxServlet?action=javaScriptAjax",true)//ture为异步请求
    //4、在send方法前绑定onreadystatechange事件，处理请求完成后的操作。
    xmlHttpRequest.onreadystatechange = function () {
        if (xmlHttpRequest.readyState == 4 && xmlHttpRequest.status == 200){
            
            var jsonObj = JSON.parse(xmlHttpRequest.responseText);
            document.getElementById("div01").innerHTML = "编号：" + jsonObj.id  + " , 姓名：" + jsonObj.name;
        }
    }
    //3、调用send方法发送请求
    xmlHttpRequest.send();
}
```



## JQuery 中的AJAX请求

### $.ajax 方法

1. url					表示请求的地址

2. type				表示请求的类型GET和POST请求

3. data				表示发送给服务器的数据

   ```
   格式有两种：
   1、name=value&name=value
   2、{key:value}
   ```

4. success			请求成功，响应的回调函数

5. dataType		数据类型		

   ```
   常用的数据类型有：
   text 	表示纯文本
   xml 	表示 xml 数据
   json 	表示 json 对象
   ```

```javascript
// ajax请求
$("#ajax_btn").click(function () {
    $.ajax({
        url:"http://localhost:8080/java_web02_war_exploded/ajaxServlet",
        data:"action=javaScriptAjax",
        type:"GET",
        success:function (data) {
            // alert("服务器返回的数据是：" + data);
            var jsonObj = JSON.parse(data);
            $("#msg").html("编号：" + jsonObj.id + " ， 姓名：" + jsonObj.name);

            //$("#msg").html("编号：" + data.id + " ， 姓名：" + data.name);
            //dataType:"json"
        },
        // "text" 表示纯文本，所以使用时需要转换为 json 对象，
        // ”json“ 就表示json对象，所以可以直接使用
        dataType:"text"
    });
});
```

### $.get 方法和 $.post 方法

1. url					请求的 url 地址

2. data				 发送的数据

3. callback		  成功的回调函数

4. type				返回的数据类型


```javascript
//ajax--get 请求
$("getBtn").click(function () {
    $.get("http://localhost:8080/java_web02_war_exploded/ajaxServlet","action=jQueryGet",function (data) {
        $("#msg").html("get 编号：" + data.id + " ，姓名：" + data.name);
    },"json");
});

//ajax--post 请求
$("postBtn").click(function () {
    $.post("http://localhost:8080/java_web02_war_exploded/ajaxServlet","action=jQueryPost",function (data) {
        $("#msg").html("post 编号：" + data.id + " ，姓名：" + data.name);
    },"json");
});
```

### $.getJSON 方法

1. url 				请求的 url 地址

2. data               发送的数据

3. callback         成功的回调函数


```javascript
//ajax---getJson请求
$("#getJSONBtn").click(function () {
    $.getJSON("http://localhost:8080/java_web02_war_exploded/ajaxServlet","action=jQueryGetJson",function (data) {
        $("#msg").html("post 编号：" + data.id + " ，姓名：" + data.name);
    })
});
```

### 表单序列化 serialize()

**serialize() 可以把表单中所有表单项的内容都获取到，并以 name=value&name=value 的形式进行拼接。**

```javascript
//ajax 请求
//serialize() 序列化
$("#submit").click(function () {
    $.getJSON("http://localhost:8080/java_web02_war_exploded/ajaxServlet","action=jQuerySerialize&" + $("#form1").serialize(),function (data) {
        $("#msg").html(" Serialize 编号：" + data.id + " ，姓名：" + data.name);
    })
});
```



# i18n

国际化标签库



基本步骤：

​	1、使用标签设置 Local 信息

​	2、使用标签设置 naseName

​	3、使用标签输出国际化信息
