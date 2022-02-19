---
title: Filter过滤器
date: 2022-01-07 
tags:
    - Filter
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

# Filter

## 1、什么是 Filter 过滤器？

1、Filter 过滤器是 JavaWeb 的三大组件之一。三大组件分别是：Serlvet程序、Listener 监听器、Filter过滤器。

2、Filter 过滤器是 JavaEE 的规范。就是接口。



拦截请求常见的应用场景有：

​	1、权限管理

​	2、日记操作

​	3、事务管理

​		.....等等



## 2、Filter 的初体验

要求：在你的 web 工程下，有一个 admin 目录。这个 admin 目录下的所有资源（html 页面、jpg图片、jsp文件、等等） 都必须是用户登录之后才允许访问。

```jsp
<%
    Object user = session.getAttribute("user");
    //如果等于null，说明还没有登录
    if (user == null){
        request.getRequestDispatcher("/login.jsp").forward(request,response);
        return;
    }
%>
```



**Filter 过滤器的使用步骤：**

1. 编写一个类去实现 Filter 接口
2. 实现过滤方法 doFilter()
3. 到 web.xml 中去配置 Filter 的拦截路径



## 3、Filter 的生命周期

Filter 的生命周期包含几个方法

1. 构造器方法

2. init 初始化方法

   第1，2步，在web工程启动的时候执行（Filter 已经创建）。

3. doFilter 过滤方法

   第 3 步，每次拦截到请求，就会执行。

4. destory 销毁方法

   第 4 步，停止 web 工程的时候，就会执行（停止 web 工程，也会销毁 Filter 过滤器）



## 4、FilterConfig 类

FilterConfig 类见名知义，它是 Filter 过滤器的配置文件类。

Tomcat 每次创建 Filter 的时候，也会同时创建一个 FilterConfig 类，这里包含了 Filter 配置文件的配置信息。

FilterConfi 类的作用：获取 Filter 过滤器的配置内容。

```java
//1、获取 Filter 的名称 filter-name 的内容
//2、获取在 Filter中配置的 init-param 初始化参数

 System.out.println("filter-name的值为：" + filterConfig.getFilterName());
        System.out.println("初始化参数 username 的值为：" + filterConfig.getInitParameter("username"));

//3、获取 ServletContext对象
```

```xml
	<!--web.xml中的配置-->
	<!--filter标签用于配置一个Filter 过滤器-->
    <filter>
		<!--给filter起一个别名-->
        <filter-name>AdminFilter</filter-name>
        <filter-class>com.lunar.web.servlet.AdminFilter</filter-class>
		<!-- 配置filter的全类名-->
        <init-param>
            <param-name>username</param-name>
            <param-value>root</param-value>
        </init-param>

    </filter>

	<!--配置filter-mapping配置Filter过滤器的拦截路径-->
    <filter-mapping>
		<!--filter-name表示当前的拦截路径给哪个filter使用-->
        <filter-name>AdminFilter</filter-name>
		<!--        
			url-pattern配置拦截
            / 同理
		-->
        <url-pattern>/admin/*</url-pattern>
    </filter-mapping>
```



## 5、FilterChain 过滤器链

Filter 过滤器

Chain 链

FilterChain，就是过滤器链（多个过滤器如何一起工作）

- 作用：

  1、执行下一个Filter过滤器（如果有Filter）

  2、执行目标资源（没有Filter）

**在多个 Filter 过滤器执行的时候，它们执行的优先顺序是由它们在 web.xml 中从上到下配置的顺序决定！**



- 多个 Filter 过滤器执行的特点：

  1、所有 Filter 和目标资源默认都执行在同一个线程中。

  2、多个 FIlter 共同执行的时候，它们都使用同一个 Request  对象。



## 6、Filter 的拦截路径

### 精确匹配

```
<url-pattern>/target.jsp</url-pattern>
以上配置的路径，便是请求地址必须为：http://ip:port/工程路径/target.jsp
```

### 目录匹配

```
 <url-pattern>/admin/*</url-pattern>
 以上配置的路径，表示请求地址必须为：http://ip:port/工程路径/admin/*
```

### 后缀名匹配

```
 <url-pattern>/*.action</url-pattern>
 以上配置的路径，表示请求地址必须以 .action 结尾才拦截到
```

Filter 过滤器它只关心请求的地址是否匹配，不关心请求的资源是否存在。

