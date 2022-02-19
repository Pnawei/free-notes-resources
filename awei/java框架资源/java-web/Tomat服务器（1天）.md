---
title: Tomcat服务器
date: 2022-01-01 
tags:
    - tomcat
    - 服务器
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

## Tomcat 是 Java-web 的一个微型服务器

### Tomcat 目录介绍

bin				  专门用来存放 Tomcat 服务器的可执行程序

conf				专门用来存放 Tomcat 服务器的配置文件

lib					专门用来存放 Tomcat 服务器的 jar 包

logs				 专门用来存放 Tomcat 服务器 运行时输出的日记信息

temp				专门用来岑放 Tomcat 运行时产生的临时数据

webapps			专门用来存放部署的 web 工程

work				是 Tomcat 工作时的目录，用来存放 Tomcat 运行时 jsp 翻译为 Serlet 的源码，和 Session 钝化的目录。(此处的钝化也就是对象序列化的意思)



### Tomcat 部署 web 工程

#### 第一种部署方式

1.到 apache 官网下载或者搜 apache-Tomcat 下载

2.解压文件

3.在 Tomat 文件下的 bin 目录下，有一个 startup.bat 可执行文件，双击打开 Tomcat 服务

​	（或者使用命令行打开，在 bin 目录下敲 cmd 进去命令行 ，输入 startup 开启服务）

4.浏览器 中 输入 http://ip:port/工程名/目录/文件名（例如http://localhost:8080/book/index.html）

【其中 http://localhost:8080 就代表进入了 webapps 目录。想要别人访问 只需要把 ip 改成自己电脑的 ip地址即可】 

#### 第二种部署方式

1.找到 Tomcat 下的 conf 目录/Catalina/localhost/ 下，创建如下的配置文件：

```xml
/*	Context 表示一个工程上下文
	path 表示工程的访问路径:/abc
	docase表示你的工程目录在哪里
*/
<Context path="/abc" dacBase="D:\book" />
```

2.后面同前面的第一种部署方式一样



### 手拖 html 页面到浏览器和在浏览器中输入 http://ip:port/工程名/目录/文件名 访问的区别

1 手拖方式 【file:///D:/java-web%E5%AD%A6%E4%B9%A0/java-01/src/book/index.html】

> 可以发现使用的file://协议
> file协议：表示告诉浏览器直接读取file协议后面的路径，解析展示在浏览器上即可。

2  http://ip:port/工程名/目录/文件名 的方式

![image-20220104142158092.png](https://s2.loli.net/2022/02/16/vjBzNUEh61aLDSM.png)



### 如何在IDEA 中部署工程到 Tomcat 上运行

**1、建议修改 web 工程对应的 Tomcat 运行实例名称：**

![image-20220104152242948.png](https://s2.loli.net/2022/02/16/VlHKDIq3MO19aQb.png)

**2、确认你的 Tomcat 实例中有你要部署运行的 web 工程模块：**

![image-20220104152802173.png](https://s2.loli.net/2022/02/16/Z3buxpS6iwEPlG5.png)

**3、使用IDEA 运行Tomcat 实例**

![image-20220104160703252.png](https://s2.loli.net/2022/02/16/sox6PlpwReAbIzC.png)