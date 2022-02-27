---
title: Listener监听器
date: 2022-01-08 
tags:
    - Listener
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

## 什么是 Listener 监听器？

1. Listener 是JavaWeb 三大组件之一。三大组件分别是：Servlet 程序、Filter 过滤器、Listener 监听器。
2. Listener 它是JavaEE 的规范，就是接口。
3. 监听器的作用是，监听某种事物的变化，然后通过回调函数，反馈给用户（程序）去做一些相应的处理。



### ServletContextListener 监听器

ServletContextListener 它可以监听 ServletContext 对象的创建和销毁。

ServletContext 对象在 web 工程启动的时候创建，在 web 工程停止的时候销毁。

监听到创建和销毁之后都会分别调用 ServletContextListener 监听器的方法反馈。

两个方法分别是：

```java
public interface ServletContextListener extends EventListener {
	/**
	* 在 ServletContext 对象创建之后马上调用，做初始化
	*/
    void contextInitialized(ServletContextEvent var1);
	/**
	* 在 ServletContext 对象销毁之后调用
	*/
    void contextDestroyed(ServletContextEvent var1);
}
```

如何使用 ServletContextListener 监听器监听 ServletContext 对象。

使用步骤如下：

1. 编写一下类去实现 ServletContextListener
2. 实现其两个回调方法
3. 到 web.xml 中去配置监听器