---
title: Cookie和Session
date: 2022-01-12 
tags:
    - cookie
    - session
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

# Cookie

## 1、什么是 Cookie？

1、Cookie 翻译过来就是饼干的意思。

2、Cookie 是服务器通知客户端保存键值对的一种技术。

3、客户端有来 Cookie 后，每次请求都发送给服务器。

4、每个 Cookie 的大小不能超过 4kb



## 2、如何创建 Cookie

```java
/**
     * 查找指定名称的 Cookie 对象
     * @param name
     * @param cookies
     * @return
     */
    public static Cookie findCookie(String name, Cookie[] cookies){
        if (name == null || cookies == null || cookies.length == 0){
            return null;
        }

        for (Cookie cookie : cookies) {
            if (name.equals(cookie.getName())){
                return cookie;
            }
        }
        return null;
    }

```



### Cookie 值得修改

方案一:

```java
//1、先创建一个修改得同名得 Cookie对象。
//2、在构造器，同时赋予新得 Cookie 值。
Cookie cookie = new Cookie("key1","newValue1");

//3、调用 response.addCookie( Cookie )。
resp.addCookie(ckooie);

```

方案二：

```java
//1、先查找到需要修改得 Cookie 对象
Cookie cookie = CookieUtils.findCookie("key2",req.getCookies());

if(cookie != null){
    //2、调用 setValue() 方法赋予新得 Cookie 值。
    cookie.setValue("newValue2");
}

//3、调用 resopnse.addCookie() 通知客户端保存。
resp.addCookie(ckooie);
```

## 3、Cookie 生命控制

Cookie 的生命控制指的是如何管理 Cookie 什么时候被销毁（删除）

单位：s

```
setMaxAge()
	正数，表示在指定的秒数后过期
	负数，表示浏览器一关，Cookie 就会被删除（默认值是-1）
	零，表示马上删除 Cookie 
```



### 免用户登录

```java
//	login.jsp
<body>
<form action="http://localhost:8080/book_war_exploded/loginServlet" method="get">
    用户名：<input type="text" name="username" value="${ cookie.username.value }"><br>
    密码：<input type="password" name="password" value=""><br>
    <input type="submit" value="提交">
</form>
</body>

//	LoginServlet.java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String username = req.getParameter("username");
    String password = req.getParameter("password");

    if ("pyw123".equals(username) && "123".equals(password)) {
       //登录 成功
       Cookie cookie = new Cookie("username", username);
       cookie.setMaxAge(60 * 60 * 24); //当前Cookie一天有效
       resp.addCookie(cookie);
       System.out.println("登录成功！");
     } else {
       //登陆 失败
       System.out.println("登录失败！");
    }
}
```

### 	

# Session 会话

## 1、什么是 Session 会话？

1、Session 就是一个接口（HttpSession）。

2、Session 就是会话。它是用于维护一个客户端和服务器之间关联的一种技术。

3、每个客户端都有自己的一个 Session 会话。

4、Session 会话中，我们经常用来保存用户保存登陆之后的信息。



## 2、如何创建 Session 和获取（id 号，是否为新）

如何创建和获取 Session。他们的 API 是一样的。

```
request.getSession() 

	第一次调用都是：创建 Session 会话

	之后调用都是：获取前面创建好的 Session 会话对象。

isNew();  判断到底是不是创建出来的（新的）

	true 表示刚创建
	false 表示获取之前创建
	
每个绘画都有一个身份证号。也就是 ID 值。而且这个 ID 是唯一的。

getId() 得到 Session 的会话 id 值。
	
```



## 3、Session 域数据的存取

```java
public class SessionServlet extends HttpServlet { /**
     * 往 Session 中保存数据
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    protected void setAttribute(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       req.getSession().setAttribute("key1","value1");
    }

    /**
     * 获取 Session 域中的数据
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    protected void getAttribute(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Object key1 = req.getSession().getAttribute("key1");
        resp.getWriter().write("从Session中获取出key1的数据是：" + key1);
    }
}
```

### Session 生命周期控制

单位 ：s

```java
public void setMaxInactiveInterval(int interval) //设置 Session 的超过时间(以 秒 为单位)，超过指定的时长，Session 就会被销毁。
	//值为正数：设定 Session 的超时时长
	//值为负数：表示永不超时（极少使用）、

public void getMaxInactiveInterval() //获取 Session 的超过时间

public void invalidate() //让当前 Session 会话马上超时无效
```

如果说，你希望你的 web 工程，默认的 Session 的超时时长为其他时长。你可以在你自己的 web.xml 配置文件中做以上相同的配置。就可以修改你的 web 工程所有 Session 的默认超时时长。

```xml
<!--表示当前 web 工程。创建出来的所有 Session 默认是 30 分钟 超时时长-->
<session-config>
	<session-timeout>30</session-timeout>
</session-config>
```

如果你想只修改个别 Session 的超时时长。就可以使用上面的 API。setMaxInactiveInterval(int interval) 来进行单独的设置。



## 4、浏览器和 Session 之间关联的技术内幕

Session 其实是基于 Cookie 实现的。

![image-20220113151743316.png](https://s2.loli.net/2022/02/16/wEeMZK8iyoWCbUT.png)