---
title: Servle程序 
date: 2022-01-06 
tags:
    - Servlet
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

## 什么是 Servlet 技术？

1. Servlet 是JavaEE规范之一。规范就是接口。
2. Servlet 是JavaWeb 三大组件之一。三大组件分别是：Servlet程序、Filter过滤器、Listener监听器。
3. Servlet 是运行在服务器上的一个 java 小程序，**它可以接收客户端发送过来的请求，并响应数据给客户端。**



## 手动实现Servlet 程序

1. 编写一个类去实现 Servlet 接口
2. 实现 service 方法，处理请求，并响应数据
3. 到 web.xml 中去配置 servlet 程序的访问地址

![image-20220104174640207.png](https://s2.loli.net/2022/02/16/8TeKJrjbyHxLVIc.png)



## Servlet 的生命周期

1. 执行 Servlet 构造器方法
2. 执行init 初始化方法
3. 执行 service 方法

4. 执行 destroy 销毁方法




## Servlet 类的继承体系

![image-20220105124354853.png](https://s2.loli.net/2022/02/16/iCNM4HgcwsoTjKG.png)



## 通过继承 HttpServlet 实现 Servlet 程序

一般在实际项目开发中，都是使用继承 HttpServlet 类的方式去实现 Servlet  程序。

1、编写一个类去继承 HttpServlet 类

```java
package com.example.webdemo;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class HelloServlet extends HttpServlet {

    /**
     * doGet() 在 get 请求的时候调用调用
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("HelloServlet 的doGet方法");
    }

    /**
     * doPost() 在 post 请求的时候调用
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("HelloServlet 的doPost方法");
    }
}
```

2、根据业务需要重写 doGet 或 doPost 方法

3、到 web.xml 中配置 Servlet 程序的访问地址【xml文件中的 Servlet 配置信息 】

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    
<!--    servlet标签给Tomcat配置Servlet程序-->
    <servlet>
<!--        servlet-name标签 Servlet程序起一个别名(一般是类名)-->
        <servlet-name>HelloServlet</servlet-name>
<!--        servlet-class是Servlet程序的全类名-->
        <servlet-class>com.example.webdemo.HelloServlet</servlet-class>
    </servlet>

<!--    servlet-mapping 标签给 servlet程序配置访问地址-->
    <servlet-mapping>
<!--        servlet-name标签的作用是告诉服务器，我当前配置的地址给哪个Servlet程序使用-->
        <servlet-name>HelloServlet</servlet-name>
<!--        url-pattern标签配置访问地址
            / 斜杠在服务器解析的时候，表示的地址：http://ip:port/工程路径名
            /hello
-->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    
</web-app>
```



## ServletConfig 类

### 三大作用

1. 可以获取 Servlet 程序的别名 servlet-name 的值

2. 获取初始化参数 init-param
3. 获取 ServletContext 对象

注意点：

```java
@Override
    public void init(ServletConfig config) throws ServletException {
        super.init(config); //一定要写调用父类
        System.out.println("重写了init初始化方法，做了一些工作");
    }
```



## SerletContext 类

### 什么是ServletContext类？

1. ServletContext是一个接口，他表示 Servlet 上下文对象
2. 一个 web 工程，只有一个 ServletContext 对象实例

3. ServletContext 对象是一个域对象



### 什么是域对象？

域对象，是可以像 Map 一样存取数据的对象，叫做域对象。

这里的域指的是存取数据的操作范围。

|        | 存数据         | 取数据         | 删除数据         |
| ------ | -------------- | -------------- | ---------------- |
| Map    | put()          | get()          | remove()         |
| 域对象 | setAttribute() | getAttribute() | removeAttibute() |

### 四个作用

1. 获取 web.xml 中配置的上下文参数 context-param
2. 获取当前的工程路径，格式: /工程路径
3. 获取工程部署后，在服务器硬盘上的绝对路径

4. 像 Map 一样存取数据


```java
//可以得到在磁盘下的路径
@WebServlet(name = "ContextServlet", value = "/ContextServlet")
public class ContextServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        ServletContext context = getServletConfig().getServletContext();
        String username = context.getInitParameter("username");
        String password = context.getInitParameter("password");
        System.out.println("context-param参数username的值是 " +  username);
        System.out.println("context-param参数password的值是 " + password);
        System.out.println("当前工程路径： " + context.getContextPath());
        /**
         * /  斜杠被服务器解析地址为:http://ip:port/工程名/  映射到 IDEA 代码的 web 目录
         */
        System.out.println("工程部署的路径是：" + context.getRealPath("/"));
        
    }
```

 

## HTTP协议

### 什么是http协议？

所谓 HTTP 协议，就是指客户端和服务器之间通信时，发送的数据，需要遵守的规则，叫做 HTTP 协议。

HTTP 协议中的数据叫做 报文，

### 请求的 HTTP 协议格式

客户端给服务器发送数据叫请求。

服务器给客户端回传数据叫响应。



请求又分为 GET 请求，和 POST 请求

#### GET请求

1、请求行

​	（1）请求的方式  											GET

​	（2）请求的资源路径[+?+请求参数]

​	（3）请求的协议的版本号								HTTP/1.1

2、请求头

​	key : value   组成		不同的键值对，表示不同的含义。

#### POST请求

1、请求行

​	（1）请求的方式  											POST

​	（2）请求的资源路径[+?+请求参数]

​	（3）请求的协议的版本号								HTTP/1.1

2、请求头

​		1）key : value   组成		不同的键值对，表示不同的含义。

​		2）空行

3、请求体 ====》 就是发送给服务器的数据



#### 哪些是 GET 请求，哪些是 POST 请求

- GET 请求有哪些：

  ```
  1、form 标签 method=get
  2、a 标签
  3、link 标签引入 js 文件
  4、Script 标签引入 js 文件
  5、img 标签引入图片
  6、iframe 引入 html 页面
  7、在浏览器地址栏中输入地址后敲回车
  ```

- POST 请求有哪些：

  ```
  form 标签 method=post
  ```



### 响应的 HTTP 协议格式

1、响应行

​	（1）响应的协议和版本号				

​	（2）响应状态码	

```
常用的响应码说明：
200			表示请求成功			
302			表示请求重定向
404			表示请求服务器已经收到了，但是你要的数据不存在(请求地址错误)
500			表示服务器已经收到请求，但是服务器内部错误(代码错误)
```

​	（3）响应状态描述符							

2、响应头

​	（1）key : value		不同的响应头，有其不同的含义

​	**空行**

3、响应体 =====》就是回传给客户端的数据



### MIME 类型说明

MINM 是 HTTP 协议中数据类型。

MIME 的英文全称是"Multipurpose Internet Mail Extensions" 多功能 Internet 邮件扩充服务。MIME 类型的格式是“大类型/小类型”，并与某一文件的扩展名相对应。



## HttpServletRequest 类

### 1、作用

每次只要有请求进入 Tomcat 服务器，Tomcat 服务器就会把请求过来的 HTTP 协议信息解析好封装到 Request对象中。

然后传递到 service 方法（doGet 和 doPost）中给我们使用，我们可以通过 HttpServletRequest 对象，获取到所有请求的信息。

### 2、常用方法

```
getRequestURL()		返回客户端发出请求时的完整 URL (绝对路径)
getRequestURI()		返回请求行中的资源名部分
getQueryString()	返回请求中的参数部分（参数名+值）
getRemoteAddr()		返回请求的客户机的 IP 地址
getRemoteHost()		返回请求的客户机的完整主机名
getRemotePort()		返回客户机所使用的网络端口号
getLocalPort()		返回 web 服务器所使用的网络端口号
getLocalAddr()		返回 Web 服务器的 IP 地址
getLocalName()		返回 Web 服务器的主机名
```

![image-20220105142038088.png](https://s2.loli.net/2022/02/16/hjFypc2WSMigokI.png)

### 3、如何获取请求参数

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String username = req.getParameter("username"); // html中的name属性值
    String password = req.getParameter("password");
    String hobby = req.getParameter("hobby");

    System.out.println("username= " + username);
    System.out.println("password= " + password);
    System.out.println("hobby= " + hobby);
}
```

### 4、请求的转发

**什么是请求的转发？**

请求转发是指，服务器收到一个请求后，从一个资源跳转到另一个资源的操作。

> 跳回注册页面；
>
> req.getRequestDispatcher("path").forward(req,resp);

![image-20220105170146886.png](https://s2.loli.net/2022/02/16/7zRGDAgCBXkowlj.png)

### 5、base 标签

> 设置页面相对路径工作时参照的地址	<base href="http://localhost:8080/工程名/路径">

### 6、Web 中 / 斜杠的不同意义

**在 web 中 / 斜杠 是一种绝对路径。**

**/（ 斜杠） 如果被浏览器解析，得到的地址是：http://ip:port/**

**映射到代码的 web 目录。**



**/ 斜杠 如果被服务器解析，得到的地址是：http://ip:port/工程路径**

```
1. <url-pattern>/servlert</url-pattern>

2. servletContext.getRealPath("/")
3. request.geRequestDispatcher("/")
```


特殊情况：request.sendRediect("/"); 	把斜杠发给浏览器解析。得到 http://ip:port/



## HttpServletResponse 类

### 1、作用

HttpServletResponse 类 和 HttpServletRequest 类一样。每次请求进来，Tomcat服务器都会创建一个 Response 对象传递给Servlet程序去使用。HttpServletRequest 表示请求过来的信息，HttpServletRespons表示所有响应的信息。

我们如果需要设置返回给客户端的信息，都可以通过 HttpServletResponse 对象进行设置。

### 2、两个输出流的说明

字节流		getOutputStream();			常用于下载 （传输二进制数据）

字符流		getWriter();				常用于回传字符串（常用）



两个流同时只能使用一个。

使用了字节流，就不能再使用字符流，反之亦然。

### 3、解决浏览器 中文乱码

```java
//推荐这种方法 
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    /**
     * 设置服务器字符集为 UTF-8
     *  resp.setCharacterEncoding("UTF-8");
     */
    //它会同时设置服务器和客户端都是用 UTF-8 字符集，还设置了响应头
    //注意：此方法一定要在获取流对象之前调用才有效
    resp.setContentType("text/html; charset=UTF-8"); //这条代码

    PrintWriter writer = resp.getWriter();
    writer.write("我的家乡在林州。");
}
```

### 4、请求重定向

是指客户端给服务器发请求，然后服务器告诉客户端说，我给你一些地址，你去新地址访问，叫请求重定向（因为之前的地址可能已经被废弃）

方案一

```
//设置响应状态码 302 ，表示重定向（已搬迁）
resp.setStatus(302);
//设置响应头，说明 新的地址在哪里
resp.setHeader("Location","http://localhost:8080");
```

方案二（推荐）

```
resp.sendRedirect("http://localhost:8080");
```

