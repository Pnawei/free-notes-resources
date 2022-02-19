---
title: jsp页面
date: 2022-01-09 
tags:
    - jsp
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

## 1、什么是 jsp，它有什么用？

jsp 的全称是 java server pages。是 Java 的服务器页面。

jsp 的主要作用是代替 Servlet 程序回传 html 页面的数据。

因为 Servlet 程序回传 html 页面数据是一件非常繁琐的事请。开发成本和维护成本都极高。



**jsp小结**

1. 创建 jsp 文件，放在 web 目录下。

2. jsp 如何访问？

   jsp 页面和 html 页面一样，都是存放在 web 目录下。访问也跟访问 html 页面一样。

```
在web目录下有如下文件：
web目录
   a.html页面		访问地址是 ==========》http://ip:port/工程路径/a.html
   b.jsp页面		访问地址是 ==========》http://ip:port/工程路径/b.jsp

```



## 2、jsp的本质是什么？

jsp 页面的本质上是一个 Servlet 程序。



当我们第一次访问 jsp 页面的时候。 Tomcat服务器会帮我们把 jsp 页面翻译成为一个 java 源文件。并且对它进行编译成为 .class 字节码程序。我们打开 java源文件 发现里面的 一个类 继承了 HttpJspBase，继续跟踪，进入源代码发现，它间接继承了 HttpServlet 类。翻译过来也说明了它就是一个 Servlet 程序。



## 3、jsp 的三种语法

### jsp 头部的 page 指令

jsp 的 page 指令可以修改 jsp 页面中一些重要的属性，或行为。

```jsp
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
```

**常用属性：**

```
1.language 属性      	 表示 jsp 翻译后是什么语言文件。暂时只支持 java。
2.contentType 属性	 表示 jsp 返回的数据类型是什么。也是源码中 response.setContentType()参数值
3.pageEncoding 属性	 表示当前 jsp 页面本身的字符集
4.import 属性	 		 跟 java 源代码中一样。用于导包，导类。
==================== 下面两个属性是 out 输出流使用======================
5.autoFush 属性	 	 设置当 out 输出流缓冲区满了之后，是否自动刷新缓冲区。默认值是true
6.errorPage 属性	 	 设置 out 缓冲 区的大小。默认是 8kb
=====================================================================
7.isErrorPage 属性	 设置当 jsp 页面运行时出错，自动跳转去的错误页面路径。 
8.session 属性	 	 设置访问房前 jsp 页面，是否会创建 HttpSession 对象。默认是true。
9.extends 属性 	 	 设置 jsp 翻译出来的 java 类默认继承谁。
```



### jsp 中的常用脚本

#### 声明脚本（极少使用）

> 声明脚本的格式是         	<%! 声明 java 代码 %>

作用：可以给 jsp 翻译出来的 java 类定义属性和方法甚至是静态代码块。内部类等。

```
练习：
1、声明类属性
2、声明 static 静态代码块
3、声明类方法
4、声明内部类

```

#### 表达式脚本（常用）

> 表达式的脚本格式是			<%=表达式%>

表达式脚本的作用是：jsp 页面上输出数据。

```
练习：
1、输出整型
2、输出浮点型
3、输出字符串
4、输出对象
```

表达式脚本的特点：

​	1、所有的表达式脚本都会被翻译到 _jspService() 方法中

​	2、表达式脚本都会被翻译成为 out.print() 输出到页面上

​	3、由于表达式脚本翻译的内容都在 _jspService() 方法中，所以 _jspService() 方法中的对象都可以直接使用。

​	4、表达式脚本中的表达式不能以分号结束。



#### 代码脚本

> 代码脚本的格式是：	<%			java语句			%>

代码脚本的作用是：可以在 jsp 页面中，编写我们所需要的功能（ 写的是 java 语句 ）。

```
练习：
1、代码脚本-----if 语句
2、代码脚本-----for 循环语句
3、翻译后 java 文件中 _jspService 方法内的代码都可以写
```

代码脚本的特点是：

​	1、代码脚本翻译之后都在 _jspService() 方法中

​	2、代码脚本由于翻译到 _jspService() 方法中，所以在 _jspService() 方法中的现有对象都可以直接使用。

​	3、还可以由多个代码脚本块组合成一个完整的 java 语句。

```jsp
<body>
<%!
    private Integer id;
    private String name;
    private String sex;
%>

<%!
    public void fun() {
        System.out.println("This is jsp-fun method.");
    }
%>

<%-- 这种就是 输出到页面中--%>
<%
    for (int i = 0; i < 10; i++) {
%>
        <%=i%> <br>
<%
    }
%>

</body>
</html>
```



### jsp 中的三种注释

1、html 注释

> <!-- 这是 html 注释 -->

html 注释会被翻译到 java 源代码中。在 _jspService 方法里，以 out.writer 输出到客户端。

2、java 注释

> <%
>
> ​		// 单行注释
>
> ​		/*	 多行注释	*/
>
> %>

java 注释会被翻译到 java 源代码中。

3、jsp 注释

> <%--  这种是 jsp 注释	--%>



## 4、jsp 九大内置对象

jsp 中的内置对象，是指 Tomcat 翻译 jsp 页面成为 Serclet 源代码后，内部提供的九大对象。

![image-20220108115015870.png](https://s2.loli.net/2022/02/16/4i8t1BUmdnoaN6f.png)

```
request			请求对象
response		响应对象
pageContext 	jsp的上下文对象
session			会话对象
application 	ServletContext对象
config 			Servletconfig对象
out				jsp输出流对象
page			指向当前jsp的对象
exception		异常对象
```



## 5、jsp 四大域对象 😊

四个域对象分别是：

```
pageContext	(PageContextImpl 类)		当前 jsp 页面范围内有效

request	(HttpServletRequest 类)		一次请求内有效

session	(HttpSession 类)				一次绘画范围内有效（打开浏览器访问服务器，直到关闭浏览器）

application	(ServletContext 类)		整个 web 工程范围内都有效（只要 web 工程不停止，数据都在）
```

域对象是可以像 Map 一样存取数据的对象。四个域对象功能一样。不同的是他们对数据存取范围。

虽然四个域对象都可以存取数据。在使用上它们是有优先顺序的。

四个域对象在使用的时候，优先顺序分别是，他们从小到大的范围的顺序。

**pageContext	=====>  request    ======>  session	=======>	application**



## 6、jsp 中的 out 输出和 response.getWriter 输出的区别

response 中表示响应，我们经常用于设置返回给客户端的内容（输出）。

out 也是给用户做输出使用的。

![image-20220108124741199.png](https://s2.loli.net/2022/02/16/wxkbCTPGt9pLRIU.png)

jsp 翻译之后，底层源码都是用 out 来进行输出，所以一般情况下，我们在 jsp 页面中统一使用 out 来进行输出。避免打乱页面输出内容的顺序。

out.write()	输出字符串都没有问题    【只适合输出字符串】

out.print()	输出任意数据都没有问题（都转换成为字符串后调用的 write 输出） 【可以输出任何数据】

**简单总结：在 jsp 页面中使用 out.print() 一定不会出错。** 



## 7、jsp 的常用标签

### jsp 静态包含

```jsp
<%--
    <%@ include file="" %> 就是静态包含
    file 属性指定你要包含的 jsp 页面的路径
    地址中第一个斜杠 / 表示为 http://ip:port/工程路径/
    映射到代码的 web 目录
    
    静态包含的特点：
        1、静态包含不会翻译被包含的 jsp 页面
        2、静态包含其实是把被包含的 jsp 页面的代码拷贝到包含的位置执行输出。
--%>

<%@ include file="/include/footer.jsp" %>
```

### jsp 动态包含

```jsp
<%--
    <jsp:include page=""></jsp:include>  这是动态包含
    page 属性是指你要包含的 jsp 页面的路径
    动态包含也可以像静态包含一样。把包含的内容执行输出到包含位置。
    
     动态包含的特点：
        1、动态包含不会翻译被包含的 jsp 页面
        2、动态包含底层代码使用如下代码去调用被包含的 jsp 页面执行输出。
        JspRuntimeLibrary.include(request,response,"/inlude/footer.jsp",out,false);
--%>
<jsp:include page="/include/footer.jsp">
	<jsp:param name="password" value="123456"/>
</jsp:include>
```

```jsp
footer.jsp 文件里

<%=request.getParameter("password")%>
```

### jsp 标签-转发

```jsp
<%--
    <jsp:forward page=""></jsp:forward> 是请求转发标签，它的功能是请求转发。
        page 属性设置请求转发路径。
--%>
<jsp:forward page="/index.jsp"></jsp:forward>
```



## 8、阶段练习题

### 1.九九乘法表

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <style type="text/css">
        table{
            width: 650px;
        }
    </style>
</head>
<body>
<h1 align="center">九九乘法表</h1>
<table align="center">
    <% for (int i = 1; i <= 9; i++) { %>
    <tr>
        <% for (int j = 1; j <= i; j++) { %>
        <td><%=j + "x" + i + "=" + (i * j) %>
        </td>
        <% } %>
    </tr>
    <% } %>
</table>

</body>
</html>
```

### 2.jsp输出一个表格，里面有10个学生信息

```jsp
<body>
<%
    ArrayList<Student> students = new ArrayList<>();
    for (int i = 0; i < 10; i++) {
        int t = i + 1;
        students.add(new Student(t, "name" + t, 18 + t, "phone" + t));
    }
%>
<table>
    <%
        for (Student student : students) {
    %>
    <tr>
        <td><%=student.getId()%></td>
        <td><%=student.getAge()%></td>
        <td><%=student.getName()%></td>
        <td><%=student.getPhone()%></td>
    </tr>
    <%
        }
    %>
</table>

</body>
```



## 9、jsp 请求转发的使用说明

![image-20220108162354864.png](https://s2.loli.net/2022/02/16/2PU5G6KnFZbHmW9.png)

```java
//SearchStudentServlet.java
@Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //获取请求参数
        //发 sql 语句查询学生信息
        //使用 for 循环生成查询到的数据做模拟
        ArrayList<Student> students = new ArrayList<>();
        for (int i = 0; i < 10; i++) {
            int t = i + 1;
            students.add(new Student(t, "name" + t, 18 + t, "phone" + t));
        }
        //保存查询到的结果（学生信息）到 request 域中
        req.setAttribute("stuList",students);
        //请求转发 showStudent.jsp 页面
        req.getRequestDispatcher("/test/showStudent.jsp").forward(req,resp);
    }

//showStudent.jsp 中主要的代码
/*
<% ArrayList<Student> students = (ArrayList<Student>) request.getAttribute("stuList"); %>
*/
```













