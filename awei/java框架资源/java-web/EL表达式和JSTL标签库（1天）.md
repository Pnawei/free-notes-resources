---
title: EL 表达式和JSTL 标签库
date: 2022-01-10 
tags:
    - EL
    - JSTL
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

# EL 表达式 & JSTL 标签库

## EL 表达式

### 1、什么是 EL 表达式，EL 表达式的作用？

EL 表达式的全称是：**Expression Lamguage**。是表达式语言。

> EL 表达式的格式是：${表达式}

```jsp
<body>
    <%
        request.setAttribute("key","值");
    %>
    表达式脚本输出key的值是：<%=request.getAttribute("key1")%>
    <br>
    EL 表达式输出key的值是：${key1}
</body>
```

EL 表达式在输出 null 值得时候，输出的是空串。jsp 表达式脚本输出 null 值得时候输出的是 null 字符串。

**EL 表达式的作用：**EL 表达式主要是代替 jsp 页面中的表达式脚本在 jsp 页面中进行数据的输出。

因为 EL 表达式再输出数据的时候，要比 jsp 表达式脚本要简洁很多。

### 2、EL 表达式搜索域数据的顺序

EL 表达式主要是在 jsp 页面中输出数据。

主要是输出域对象中的数据。

当四个域中都有相同的 key 的数据的时候，EL 表达式会按照四个域的从小到大的顺序去进行搜索，找到就输出。

### 3、EL 表达式使出 Bean 的普通属性，数组属性。List 集合属性，map 集合属性。

需求---输出 Person 类中普通属性，数组属性。list 集合属性和 map 集合属性。

```jsp
<body>

<%--
    Person.java 属性
    private String name;
    private String[] phones;
    private List<String> cities;
    private Map<String,Object> map;
--%>
<%
    Person person = new Person();
    person.setName("我的家乡是林州。");
    person.setPhones(new String[]{"123123345","123345123","123532454356"});

    List<String> cities = new ArrayList<>();
    cities.add("北京");
    cities.add("上海");
    cities.add("深圳");
    person.setCities(cities);

    Map<String, Object> map = new HashMap<>();
    map.put("key1","value1");
    map.put("key2","value2");
    map.put("key3","value3");
    person.setMap(map);

    session.setAttribute("person",person);
%>

    输出Person：${person}<br>
    输出Person的name属性值:${person.name}<br>
    输出Person的phones数组属性值：${person.phones[0]}<br>
    输出Person的cities集合中的某一个元素值：${person.cities[1]} <br>
    输出Person的Map集合中的某个key：${person.map.key1}

</body>
```

### 4、EL 表达式 ------- 运算

> 语法： ${ 运算表达式 } 

#### 关系运算

| 关系说明 |   说明   |              范例              | 结果  |
| :------: | :------: | :----------------------------: | :---: |
| == 或 eq |   等于   | ${  5 == 5  } 或 ${  5 eq 5  } | true  |
| != 或 ne |  不等于  | ${  5 != 5 } 或 ${  5 ne 5  }  | false |
| < 或 lt  |   小于   | ${  3 < 5  } 或 ${  3 lt 5  }  | true  |
| > 或 gt  |   大于   | ${  2 > 10 } 或 ${  2 gt 10 }  | false |
| <= 或 le | 小于等于 | ${  5 <= 12 } 或 ${  5 le 12 } | true  |
| >= 或 ge | 大于等于 | ${  3 >= 5  } 或 ${  3 ge 5  } | false |

#### 逻辑运算

|  逻辑运算  |   说明   |                          范例                          | 结果  |
| :--------: | :------: | :----------------------------------------------------: | :---: |
| && 或 and  |  与运算  | ${ 12 == 12 && 12 < 11 } 或 ${ 12 == 12 and 12 < 11 }  | false |
| \|\| 或 or |  或运算  | ${ 12 == 12 \|\| 12 < 11 } 或 ${ 12 == 12 or 12 < 11 } | true  |
|  ! 或 not  | 取反运算 |              ${ ! true } 或 ${ not true}               | false |

#### 算术运算

| 算术运算 | 说明 |                  范例                  | 结果 |
| :------: | :--: | :------------------------------------: | :--: |
|    +     | 加法 |              ${ 12 + 18 }              |  30  |
|    -     | 减法 |              ${ 18 - 8 }               |  10  |
|    *     | 乘法 |              ${ 12 * 12}               | 144  |
| / 或 div | 除法 | ${ 144 / 12 } 或 ${ 144  **div**  12 } |  12  |
| % 或 mod | 取模 | ${ 144 % 10 } 或 ${ 144  **mod**  10}  |  4   |



##### （1）empty 运算

empty 运算可以判断一个数据是否为空，如果为空，则输出 true，不为空输出 false。

**以下几种情况为 空：**

1. 值为 null 值的时候，为空
2. 值为 空串 的时候，为空
3. 是Object 类型数组，长度为零的时候
4. list 集合，元素个数为零
5. map 集合，元素个数为零

##### （2）三元运算

表达式1 ? 表达式2 : 表达式3

##### （3）" . " 点运算 和 " [ ] "中括号运算符

 点运算，可以输出 Bean对象中某个属性的值。

[] 中括号运算，可以输出有序集合中某个元素的值。

并且 [] 中括号运算，还可以输出 map 集合中 key 里含有特殊字符的 key的值。 

### 5、EL 表达式的 11 个隐含对象

EL 表达式中 11 个隐含对象，是 EL 表达式中自己定义的，可以直接使用。

| 变量             | 类型                 | 作用                                                       |
| :--------------- | :------------------- | :--------------------------------------------------------- |
| pageContext      | PageContextImple     | 它可以获取 jsp 中的九大内置对象                            |
| pageScope        | Map<String,Object>   | 它可以获取 pageContext 域中的数据                          |
| requestScope     | Map<String,Object>   | 获取 Request 域中的数据                                    |
| sessionScope     | Map<String,Obiect>   | 它可以获取 Session 域中的数据                              |
| applicationScope | Map<String,Obiect>   | 它可以获取 ServletContext 域中的数据                       |
| param            | Map<String,Obiect>   | 它可以获取 请求参数的值                                    |
| paramValues      | Map<String,String[]> | 它可以获取 请求参数的值，获取多个值的时候使用              |
| header           | Map<String,String>   | 它可以获取请求头的信息                                     |
| headerValues     | Map<String,String[]> | 它可以获取请求头的信息，它可以获取多个值的情况             |
| cookie           | Map<String,Cookie>   | 它可以获取当前请求的 Cookie 信息                           |
| initParam        | Map<String,String>   | 它可以获取在 web.xml 中配置的 `<context-param>` 上下文参数 |

#### EL 获取四个特定域中的属性

pageScope                       ===========                     pageContext 域

requestScope				  ===========                     Request 域

sessionScope				   ===========                     Session 域

applicationScope			===========                     ServletContext 域

#### pageContext 对象的使用

```jsp
<body>

1. 协议； ${ pageContext.request.scheme }<br>
2. 服务器 ip；${ pageContext.request.serverName}<br>
3. 服务器端口； ${ pageContext.request.serverPort}  <br>
4. 获取工程路径； ${ pageContext.request.contextPath} <br>
5. 获取请求方法； ${ pageContext.request.method} <br>
6. 获取客户端 ip 地址； ${pageContext.request.remoteHost}<br>
7. 获取会话的 id 编号； ${ pageContext.session.id}<br>

</body>
```

#### EL 表达式奇特隐含对象的用法

1. param		              ${  param.username  }
2. paramvalues           ${  param.hobby[0]   }
3. header                      ${   header['User-Agent']    }
4. headervalues           ${ header['User-Agent'] [0]     }
5. cookie                        输出Cookie的名称 ${ cookie.JSESSIONID.name }
6. initParam                  ${  initParam.username  }



## JSTL 标签库

JSTL 标签库全称为 JSP Standard Tag Library 。 是 JSP 标准标签库。是一个不断完善的开放源代码的 JSP标签库。

EL 表达式主要是为了 替换 jsp 中的表达式脚本，而标签库则视为了替换代码 脚本。这样使得整个 jsp 页面变得更加简洁。

JSTL 由五个不同功能的标签库组成。

| 功能范围                | URI                                    | 前缀 |
| ----------------------- | -------------------------------------- | ---- |
| **核心标签库（重点）**😊 | http://java.sun.com/jsp/jstl/core      | c    |
| 格式化                  | http://java.sun.com/jsp/jstl/fmt       | fmt  |
| 函数                    | http://java.sun.com/jsp/jstl/functions | fn   |
| 数据库（不使用）        | http://java.sun.com/jsp/jstl/sql       | sql  |
| XML（不使用）           | http://java.sun.com/jsp/jstl/xml       | x    |

### 1、JSTL 标签库的使用步骤

1、先导入 jstl 标签库的 jar 包。

```
taglibs-standard-impl-1.2.5.jar
taglibs-standard-spec-1.2.5.jar
```

2、使用 taglib 指令引入标签库。

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

### 2、core 核心库使用 😊

#### <c:set /> 标签

```jsp
<body>
<%--
    域对象.setAttribute(key,value);
    scope 属性设置保存到哪个域
        page 表示pageContext域 (默认)
        request 表示Request域
        session 表示Session域
        application 表示SerletContext域
        var属性设置 key是多少
        value属性设置 值
--%>
保存之前：${ requestScope.abc } <br>
<c:set scope="request" var="abc" value="abcValue" />
保存之后：${ requestScope.abc } <br>

</body>
```

#### <c:if ></ c:if> 标签

```jsp
<%--
    test里面的条件为true，则显示里面内容，为false则不显示
--%>
<c:if test="${12 == 12}">
    <h1>12等于12</h1>
</c:if>
```

#### <c:choose > <c:when > <c:otherwise > 标签 

作用：多路判断。跟 switch...case...default 非常接近。

```jsp
<body>
<%
    request.setAttribute("height",178);
%>
<c:choose>
    <c:when test="${ requestScope.height > 170}">
        <h1>您的身高大于170,真棒!</h1>
    </c:when>
    <c:when test="${ requestScope.height == 170}">
        <h1>您的身高等于于170,真棒!</h1>
    </c:when>
</c:choose>
</body>
```

#### <c:forEach >

作用：遍历输出使用。

1、遍历 1 到 10，输出

```jsp
<body>
<%--  1、遍历 1 到 10，输出
        begin 属性设置开始的索引
        end 属性设置结束的索引
        var 属性表示循环的变量(也是当前正在遍历到的数据)
        for(int i=0 ; i < 10 ; i++)
--%>
    <table border="1">
        <c:forEach begin="1" end="10" var="i">
            <tr>
                <td>
                    第 ${ i } 行
                </td>
            </tr>
        </c:forEach>
    </table>
</body>
```

2、遍历 Obiect 数组

```jsp
<%--    2、遍历 Obiect 数组
    for(Object item: arr)
    items 表示遍历的数据源(遍历的集合)
--%>
<hr>
<%
    request.setAttribute("arr",new String[]{"1231123","567567567","890807678"});
%>
<c:forEach items="${ requestScope.arr}" var="item">
    ${item} <br>
</c:forEach>
```

3、遍历 List 集合----list 中存放 Person 类，有属性：编号，用户名，密码，年龄，电话信息

```jsp
<%
    Map<String, Object> map = new HashMap<>();
    map.put("key1","value1");
    map.put("key2","value2");
    map.put("key3","value3");
    request.setAttribute("map",map);
%>
<c:forEach items="${ requestScope.map }" var="entry">
    ${entry} <br>
</c:forEach>
```

4、遍历 Map 集合

```jsp
<%
    List<Student1> studentList = new ArrayList<>();
    for (int i = 1; i <= 10; i++) {
        studentList.add(new Student1(i ,"username"+i , "password"+i , 18+i , "phone"+i));
    }
    request.setAttribute("stus",studentList);
%>
<table>
    <tr>
        <th>编号</th>
        <th>用户名</th>
        <th>密码</th>
        <th>年龄</th>
        <th>电话</th>
        <th>操作</th>
    </tr>
    <%--
        items 表示遍历的集合
        var 表示遍历到的数据
        begin 表示遍历的开始索引值
        end 表示结束的索引值
     `   setp 表示遍历的步长值
    --%>
    <c:forEach items="${ requestScope.stus }" var="stu">
    <tr>
        <td>${ stu.id }</td>
        <td>${ stu.name }</td>
        <td>${ stu.password }</td>
        <td>${ stu.age }</td>
        <td>${ stu.phone }</td>
        <td>删除、修改</td>
    </tr>
    </c:forEach>
</table>
```





