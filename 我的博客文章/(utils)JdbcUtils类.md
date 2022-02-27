---
title: Jdbc数据库连接类 
date: 2021-12-30
tags: 
    - 工具类
    - jdbc
    - Java
---

该工具类中有两个方法：

（1） 一是数据库的连接 getConnection() 方法

（2） 二是数据库关闭 release() 方法

<!-- more -->

## 数据库连接类 JDBCUtils

1、创建一个 db.properties  文件存放

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/test
username=root
password=root123
```

2、创建一个 JdbcUtiles 类

```java
package com.lunar.utils;

import java.sql.*;
import java.util.ResourceBundle;

@SuppressWarnings({"all"})
public class JdbcUtils {

    //数据库url、用户名和密码
    private static String driver;
    private static String url;
    private static String username;
    private static String password;

    /**
     * 读取属性文件，获取jdbc信息
     */
    static {
        ResourceBundle bundle = ResourceBundle.getBundle("db");
        driver = bundle.getString("driver");
        url = bundle.getString("url");
        username = bundle.getString("username");
        password = bundle.getString("password");
    }

    public static Connection getConnection() {
        Connection conn = null;
        try {
            //1、注册JDBC驱动
            Class.forName(driver);
            // 2、获取数据库连接 
            conn = DriverManager.getConnection(url, username, password);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return conn;
    }

    /**
     * 关闭结果集、数据库操作对象、数据库连接
     */
    public static void release(Connection connection, PreparedStatement preparedStatement, ResultSet resultSet) {

        if (resultSet != null) {
            try {
                resultSet.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (preparedStatement != null) {
            try {
                preparedStatement.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (connection != null) {
            try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {

    }
}

```

