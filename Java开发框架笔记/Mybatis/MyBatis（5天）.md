---
title: MyBatis
date: 2022-01-31 
tags:
    - MyBatis
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

# 一、MyBatis入门 + 接口式编程（idea实现）

## 1、工程的目录结构

由于是入门级 demo，所以直接弄个 java 工程，也不用 maven 了 。 

![clipboard _18_.png](https://s2.loli.net/2022/02/16/BnkCWocjFeJ5Kh1.png)

> 注意：
>
> 1、需要将 jar 包导入到工程模块中
>
> 2、需要将 conf 目录标注为资源文件。方法：鼠标右键 + Mark Directory as ...



## 2、java bean

```java
package com.atguigu.mybatis.bean;

public class Employee {
   
   private Integer id;
   private String lastName;
   private String email;
   private String gender;
   
   public Integer getId() {
      return id;
   }
   public void setId(Integer id) {
      this.id = id;
   }
   public String getLastName() {
      return lastName;
   }
   public void setLastName(String lastName) {
      this.lastName = lastName;
   }
   public String getEmail() {
      return email;
   }
   public void setEmail(String email) {
      this.email = email;
   }
   public String getGender() {
      return gender;
   }
   public void setGender(String gender) {
      this.gender = gender;
   }
   @Override
   public String toString() {
      return "Employee [id=" + id + ", lastName=" + lastName + ", email="
            + email + ", gender=" + gender + "]";
   }
} 
```



## 3、mybatis的全局配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
 PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
   <environments default="development">
      <environment id="development">
         <transactionManager type="JDBC" />
         <dataSource type="POOLED">
            <property name="driver" value="com.mysql.jdbc.Driver" />
            <property name="url" value="jdbc:mysql://localhost:3306/mybatis" />
            <property name="username" value="root" />
            <property name="password" value="root" />
         </dataSource>
      </environment>
   </environments>
   <!-- 
		将我们写好的 sql 映射文件（EmployeeMapper.xml）
   		一定要注册到全局配置文件（mybatis-config.xml）中 
	-->
   <mappers>
      <mapper resource="EmployeeMapper.xml" />
   </mappers>
</configuration>            
```

## 4、sql映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
 PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.atguigu.mybatis.mapper.EmployeeMapper">
<!-- 
namespace:名称空间; 指定为接口的全类名
id：唯一标识
resultType：返回值类型
#{id}：从传递过来的参数中取出id值

public Employee getEmpById(Integer id);
 -->
   <select id="getEmpById" resultType="com.atguigu.mybatis.bean.Employee">
      select id,last_name lastName,email,gender from tbl_employee where id = #{id}
   </select>
</mapper>
```

## 5、log4j 的配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
 
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
 
 <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
   <param name="Encoding" value="UTF-8" />
   <layout class="org.apache.log4j.PatternLayout">
    <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS} %m  (%F:%L) \n" />
   </layout>
 </appender>
 <logger name="java.sql">
   <level value="debug" />
 </logger>
 <logger name="org.apache.ibatis">
   <level value="info" />
 </logger>
 <root>
   <level value="debug" />
   <appender-ref ref="STDOUT" />
 </root>
</log4j:configuration>
```

## 4、mapper 接口

```java
public interface EmployeeMapper {

    public Employee getEmpById(int id);
}
```

## 5、测试代码

```java
/*
    1、sqlSession代表和数据库的一次会话，用完必须关闭
    2、SqlSession是非线程安全的，每次使用都应该创建一个新的对象
    3、mapper接口没有实现类，但是mybatis会为这个接口生成一个代理对象
    4、两个重要的配置文件：
        mybatis的全局配置文件
        sql映射文件
 */
public class MybatisTest {

    public SqlSessionFactory getSqlSessionFactory() throws IOException {
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        return sqlSessionFactory;
    }

    /*
     * 1、根据xml配置文件（mybatis的全局配置文件）创建一个SqlSessionFactory对象
     * 2、sql映射文件
     * 3、将sql映射文件注册到mybatis全局配置文件
     */
    @Test
    public void test() throws IOException {
        SqlSession openSession = getSqlSessionFactory().openSession();
        try {
            Employee employee = openSession.selectOne(
                    "com.atguigu.mybatis.dao.EmployeeMapper.getEmpById", 1);
            System.out.println(employee);
        } finally {
            openSession.close();
        }
    }

    @Test
    public void testMapper() throws IOException {
        SqlSession openSession = getSqlSessionFactory().openSession();
        EmployeeMapper mapper = openSession.getMapper(EmployeeMapper.class);
        Employee e = mapper.getEmpById(1);
        System.out.println(e);
    }
}
```

​	![clipboard _19_.png](https://s2.loli.net/2022/02/16/L5dfvH1pFQacEtI.png)





# 二、全局配置文件详解

## 1、peoperties——配置文件

mybatis 可以使用 properties 来引入外部 properties 配置文件的内容

> **resource**：引入类路径下的资源
>
> **url**：引入网络或者磁盘路径下的资源

**db.properties：**

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/mybatis 
jdbc.username=root 
jdbc.password=root      
```

​    ![clipboard _20_.png](https://s2.loli.net/2022/02/16/p8Nrq5QF1CnilT9.png)



## 2、settings——设置项

这是 mybatis 中极为重要的调整设置，他们会改变 mybatis 的运行时行为

```xml
<!-- 设置转驼峰
settings：所有的设置项
setting ：每个设置项
-->
<settings>
   <setting name="mapUnderscoreToCamelCase" value="true"/>
</settings>
```



## 3、typeAliase——取别名

```xml
<!--别名处理器 typeAliases 为某个类型起别名  别名不区分大小写-->
<typeAliases>
   <!--
   typeAlias : 为某个java类型取别名
      type: 指定要娶别名的类型的全类名，默认别名时类名小写employee
      alias: 指定新的别名
   -->
   <!--<typeAlias type="com.atguigu.mybatis.bean.Employee" alias="emp"></typeAlias>-->

   <!--批量起别名
      name :指定包名（为当前包已经下面所有子包的所有类起一个默认别名，类名小写）
   -->
   <package name="com.atguigu.mybatis.bean"/>
</typeAliases>
```



## 4、typeHandlers——类型处理器





## 5、plugins——插件简介

​    ![0](https://note.youdao.com/yws/public/resource/268f6d5851fd1928866d1daca38c4c60/xmlnote/D434E167BEAC4A3F8ED7EF409B719E4C/28278)



## 6、environments——环境变量

```xml
<!--
   mybatis 可以配置多种环境  default指定使用某种环境
   environment ：配置具体的环境信息，必须有两个标签：transactionManager dataSource
      id: 是环境的唯一标识
      transactionManager： 事务管理器
         type : JDBC|MANAGED 事务管理器的类型

      dataSource: 数据源
         type: UNPOOLED|POOLED|JNDI


-->
<environments default="development">
   <environment id="development">
      <transactionManager type="JDBC" />
      <dataSource type="POOLED">
         <property name="driver" value="${jdbc.driver}" />
         <property name="url" value="${jdbc.url}" />
         <property name="username" value="${jdbc.username}" />
         <property name="password" value="${jdbc.password}" />
      </dataSource>
   </environment>
</environments>
```



## 7、databaseIdProvider——多数据库支持

```xml
<!--
   databaseIdProvider : 支持多数据库厂商

   mybatis 根据数据库厂商的标识来执行不同的sql

-->
<databaseIdProvider type="DB_VENDOR">
   <property name="MySQL" value="mysql"/> //支持mysql环境
   <property name="Oracle" value="oracle"/> //支持oracle环境
</databaseIdProvider>
```



  **databaseId**：告诉 mybatis 这条语句是在什么环境下执行的  

```xml
<select id="getEmpById" resultType="employee" databaseId="mysql">  
    select id,last_name,email,gender from tbl_employee where id = #{id}
</select>          
```

​    

## 8、mappers——映射文件

```xml
<!-- 将我们写好的sql映射文件（EmployeeMapper.xml）
一定要注册到全局配置文件（mybatis-config.xml）中 -->
<!--
   将sql映射注册到 mybatis 全局配置文件中
   mapper: 注册一个sql映射
      resource：引用类路径下的sql映射文件
      url : 引用网络路径或者磁盘路径下的sql映射文件

      class : 引用接口
         1、映射文件名和接口同名，并且与接口放在同一路径下
         2、没有sql映射文件，所有的sql都是利用注解写在接口上

         推荐：
         比较重要的，复杂的dao接口，我们来写sql映射文件
         不重要，简单的sql文件我们利用注解写在接口上

      package: 批量注册
      映射文件名和接口同名，
      并且与接口放在同一路径下

-->
<mappers>
   <!--<mapper resource="EmployeeMapper.xml" />-->
   <!--<mapper class="com.atguigu.mybatis.mapper.EmployeeMapper"></mapper>-->
   <package name="com.atguigu.mybatis.mapper"/>
</mappers>
```





# 三、Mybatis_映射文件

## 1、insert——获取自增主键的值

```xml
<!-- 增加
    mybatis 也是利用 statement.getGeneratedKeys()来获取自增主键值
    useGeneratedKeys ="true" 使用自增主键获取主键值策略
    keyProperty : mybatis获取到主键值后，将其封装到java bean的哪个属性
-->
<insert id="addEmp" parameterType="com.atguigu.mybatis.bean.Employee" useGeneratedKeys="true"
   keyProperty="id">
   insert into tbl_employee(last_name,email,gender)
   values(#{lastName},#{email},#{gender})
</insert>
```

 

## 2、insert：获取非自增主键的值 selectKey

```xml
<!--
     oracle 不支持自增： Oracle 使用序列来模拟自增
     每次插入的数据的主键是从序列中拿到的值，那么如何获取到这个值
-->
<insert id="addEmp" databaseId="oracle">
    /*
    keyProperty: 查出的主键值封装到javaBean的哪个属性
    order = "BEFORE" 当前sql在插入sql之前运行
    "AFTER"  当前sql在插入sql之后运行
    resultType : 查出的数据的返回值类型
    */
    <selectKey keyProperty="id" order="BEFORE" resultType="Integer">
        /*编写查询主键的sql语句*/
        select employees_seq.nextval from dual;
    </selectKey>
    /*插入的主键是从序列中拿到的*/
    insert into employees(id,last_name,email,gender)
    values(#{lastName},#{email},#{gender})
</insert>
```



## 3、mybatis 参数处理

**单个参数：**

​			mybatis不会做特殊处理，#{参数名} 取出参数

**多个参数**：

​	mybatis会做特殊处理

​	多个参数会被封装成一个map

​			key：param1...paramN

​			value: 对应的按照顺序传入的参数

​			#{param1} 就是从 map 中获取指定的值

**命名参数：**

​		明确指定封装参数时map的key  ==》接口定义时：

​		多个参数会被封装成一个map

​				key：使用@param注解指定的值

​				value：参数值

​				#{key} 就是从map中获取指定的值



接口中的方法：

```java
 public Employee getEmpByIdAndLastName(@Param("id") int id, @Param("lastName") String lastName);  
```



mapper.xml中   

```xml
<select id="getEmpByIdAndLastName" resultType="employee">   
    select id,last_name,email,gender from tbl_employee    
    where id = #{id} and last_name =#{lastName} 
</select>          
```

​    ![clipboard _21_.png](https://s2.loli.net/2022/02/16/o98WJ4ebrqYxM1Q.png)

**POJO：**

如果多个参数正好是我们业务逻辑的数据原型，可以之间传入pojo

\#{属性名} 取出对应的值

**Map:**

如果多个参数不是业务模型中的数据，没有对应的pojo，为了方便，我们也可以传入map

\#{key} 取出对应的值

**应用示例**

​    ![clipboard _22_.png](https://s2.loli.net/2022/02/16/FoWEyajTpYX7cxQ.png)

**参数值的获取**

**#{}** ：以预编译的形式，将参数设置到sql语句中，类似于jdbc的参数占位符，防止sql注入

**${}** :   取出的值直接拼装在sql语句中，会有安全问题

**#{} 更丰富的用法**

规定参数的一些规则：

​	javaType、 jdbcType、 mode（存储过程）、 numericScale、

​	resultMap、 typeHandler、 jdbcTypeName、 expression（未来准备支持的功能）；

​	

​	jdbcType通常需要在某种特定的条件下被设置：

​		  在我们数据为null的时候，有些数据库可能不能识别mybatis对null的默认处理。比如Oracle（报错）；

​		

​		  JdbcType OTHER：无效的类型；因为mybatis对所有的null都映射的是原生Jdbc的OTHER类型，oracle不能正确处理;

 		

​		 由于全局配置中：jdbcTypeForNull=OTHER；oracle不支持；两种办法

​		 1、#{email,jdbcType=NULL };

​		 2、jdbcTypeForNull=NULL	 `<setting name="jdbcTypeForNull" value="NULL"/>`



## 4、select 返回 list 和 map

如果 select 返回 list，resultType 取得是 list 中的泛型

如果 select 返回 map，resultType = "map"



## 5、select_resultMap

**自定义结果映射规则：**

```xml
<resultMap id="myemp" type="com.atguigu.mybatis.bean.Employee">
    <!--指定主键列的封装规则
    id 定义主键，底层会有优化
    column :指定哪一列
    property: 指定对应的javaBean属性
    -->
    <id column="id" property="id"></id>
    <result column="last_name" property="lastName"></result>
</resultMap>

<select id="getEmpById" resultMap="myemp">
    select * from tbl_employee where id = #{id}
</select>
```

  

**级联属性封装结果：**

```xml
<resultMap id="myEmpDept" type="com.atguigu.mybatis.bean.Employee">
    <id column="id" property="id"></id>
    <result column="last_name" property="lastName"></result>
    <result column="gender" property="gender"></result>
    <result column="email" property="email"></result>
    <result column="did" property="dept.id"></result>
    <result column="dept_name" property="dept.deptName"></result>
</resultMap>

<select id="getEmpAndDept" resultMap="myEmpDept">
    select
    e.id id,
    e.last_name last_name,
    e.gender gender,
    e.email email,
    d.id did,
    d.dept_name dept_name
    from  tbl_employee e left join tbl_dept d
    on e.dept_id = d.id
    where e.dept_Id = 2
</select>
```

​           

【注意】Employee中有一个Department对象

​    ![clipboard _23_.png](https://s2.loli.net/2022/02/16/e5vxkXrW2HIlZof.png)

结果：

​    ![clipboard _24_.png](https://s2.loli.net/2022/02/16/ogFHvwNP47iJDT1.png)

 

**association定义关联对象封装规则：**

```xml
<!--
    使用 association ，封装关联的单个对象
-->
<resultMap id="myEmpDept1" type="com.atguigu.mybatis.bean.Employee">
    <id column="id" property="id"></id>
    <result column="last_name" property="lastName"></result>
    <result column="gender" property="gender"></result>
    <result column="email" property="email"></result>

    <!-- association 可以指定联合的javaBean对象
         property : 指定哪个属性是联合的对象
         javaType : 指定这个属性对象的类型
    -->
    <association property="dept" javaType="com.atguigu.mybatis.bean.Department">
        <result column="did" property="id"></result>
        <result column="dept_name" property="deptName"></result>
    </association>
</resultMap>

<select id="getEmpAndDept" resultMap="myEmpDept1">
    select
    e.id id,
    e.last_name last_name,
    e.gender gender,
    e.email email,
    d.id did,
    d.dept_name dept_name
    from  tbl_employee e left join tbl_dept d
    on e.dept_id = d.id
    where e.dept_Id = #{id}
</select>
```

​        

也是一样的结果

​    ![clipboard _26_.png](https://s2.loli.net/2022/02/16/5tVf9P8dJvpcRNU.png)



**association分步查询**

1）先准备好department对象的mapper和 xml文件

​    ![clipboard _27_.png](https://s2.loli.net/2022/02/16/tQYgURI4udia2JT.png)

DepartmentMapper.xml

```xml
<select id="getDeptById" resultType="com.atguigu.mybatis.bean.Department">
   select id,dept_name deptName from tbl_dept where id =#{id}
</select>
```

​        

EmployeeMapperPlus.xml

```xml
<!-- association 分步查询-->
<resultMap id="myEmpDept2" type="com.atguigu.mybatis.bean.Employee">
    <id column="id" property="id"></id>
    <result column="last_name" property="lastName"></result>
    <result column="gender" property="gender"></result>
    <result column="email" property="email"></result>

    <!-- association 可以指定联合的javaBean对象
         property : 指定哪个属性是联合的对象
         select: 调用目标的方法查询当前属性的值
         column: 将sql中的哪一列传入上述调用的方法
    -->
    <association property="dept" select="com.atguigu.mybatis.mapper.DepartmentMapper.getDeptById" column="dept_id">
    </association>
</resultMap>

<select id="getEmpAndDept" resultMap="myEmpDept2">
    select
    e.id id,
    e.last_name last_name,
    e.gender gender,
    e.email email,
    e.dept_id
    from  tbl_employee e 
    where e.dept_Id = #{id}
</select>
```

​          

结果：

​    ![clipboard _28_.png](https://s2.loli.net/2022/02/16/85QR1kw2hgdm3BP.png)



**分步查询&延迟加载**

只有在真正用到关联对象时，才会进行第二次的分布查询

```xml
<settings>
   <setting name="lazyLoadingEnabled" value="true"/>
   <setting name="aggressiveLazyLoading" value="false"/>
</settings>
```

​    ![clipboard _29_.png](https://s2.loli.net/2022/02/16/5bnAC7YWDwmzJxR.png)



**collection定义关联集合封装规则**

```xml
<resultMap id="myDept" type="com.atguigu.mybatis.bean.Department">
   <id column="did" property="id"></id>
   <result column="dept_name" property="deptName"></result>

   <!--
      collection 定义集合类型属性的封装规则
      ofType: 集合中元素的类型
   -->
   <collection property="emps" ofType="com.atguigu.mybatis.bean.Employee">
      <!--定义集合中元素的封装规则-->
      <id column="eid" property="id"></id>
      <result column="last_name" property="lastName"></result>
      <result column="email" property="email"></result>
      <result column="gender" property="gender"></result>
   </collection>
</resultMap>

<select id="getgetDeptByIdPlus" resultMap="myDept">
   select 
   d.id did,
   d.dept_name dept_name,
   e.id eid,
   e.last_name last_name,
   e.email email,
   e.gender gender
   from tbl_dept d
   left join tbl_employee e
   on d.id =e.dept_id
   where d.id =#{id}
</select>
```



**collection分步查询和延迟加载**

```
 <!--collection 分步查询-->
<resultMap id="myDeptStep" type="com.atguigu.mybatis.bean.Department">
   <id column="id" property="id"></id>
   <result column="dept_name" property="deptName"></result>
   <collection property="emps" select="com.atguigu.mybatis.mapper.EmployeeMapper.getEmpsByDeptId" column="id">

   </collection>
</resultMap>

<select id="getgetDeptByIdStep" resultMap="myDeptStep">
   select id,dept_name from tbl_dept where id =#{id}
</select>           
```

​    ![clipboard _30_.png](https://s2.loli.net/2022/02/16/melDnNj4OuaIXYq.png)



**扩展：分步查询select中方法，如果要传多列的值：**

​			将多列的值封装成map传递

​			column = "{k1= column1}"

​			fetchType ="lazy"：表示延迟加载

​					-lazy :延迟加载

​					-eager: 立即查询

```xml
<collection property="emps" select="com.atguigu.mybatis.mapper.EmployeeMapper.getEmpsByDeptId" column="id" fetchType="lazy"> </collection>       
```

​       





# 四、Mybatis_动态sql

## 1、if 标签

```xml
<select id="getEmpsByConditionIf" resultType="com.atguigu.mybatis.bean.Employee">
   select * from tbl_employee
   where 1=1
   <if test="id!=null">
      and id = #{id}
   </if>
   <if test="lastName!=null and lastName !=''">
      and last_name like '%${lastName}%'
   </if>
   <if test="email!=null">
      and email like  '%${email}%'
   </if>
   <if test="gender==0 or gender == 1">
      and gender = #{gender}
   </if>
</select>
```

​    ![clipboard _31_.png](https://s2.loli.net/2022/02/16/D6rgXiV5dmZQ1FU.png)



## 2、where标签

去除动态sql中多余的and 和 or

```xml
<select id="getEmpsByConditionIf" resultType="com.atguigu.mybatis.bean.Employee">
   select * from tbl_employee
   <where>
      <if test="id!=null">
         and id = #{id}
      </if>
      <if test="lastName!=null and lastName !=''">
         and last_name like '%${lastName}%'
      </if>
      <if test="email!=null">
         and email like  '%${email}%'
      </if>
      <if test="gender==0 or gender == 1">
         and gender = #{gender}
      </if>
   </where>
</select>
```

​      

## 3、trim 字符串截取

```xml
<select id="getEmpsByConditionTrim" resultType="com.atguigu.mybatis.bean.Employee">
   select * from tbl_employee
   <!--
      后面多出的and or where 标签不能解决
      trim标签体中是整个字符串拼拼接后的结果

      prefix：给拼串后的字符串加一个前缀
      prefixOverrides="" : 前缀覆盖 去掉整个字符串前面多余的字符串
      suffixOverrides="" : 后缀覆盖 去掉整个字符串后面多余的字符串
   -->
   <trim prefix="where" suffixOverrides="and">
      <if test="id!=null">
         id = #{id} and
      </if>
      <if test="lastName!=null and lastName !=''">
         last_name like '%${lastName}%' and
      </if>
      <if test="email!=null">
         email like  '%${email}%' and
      </if>
      <if test="gender==0 or gender == 1">
         gender = #{gender} and
      </if>
   </trim>
</select>
```

​       

## 4、choose when

```xml
<select id="getEmpsByConditionChoose" resultType="com.atguigu.mybatis.bean.Employee">
   select * from tbl_employee
   <where>
      <choose>
         <when test="id!=null">
            and id = #{id}
         </when>
         <when test="lastName!=null and lastName !=''">
            and last_name like '%${lastName}%'
         </when>
         <otherwise>
            and gender = 1
         </otherwise>
      </choose>
   </where>
</select>
```

![clipboard _32_.png](https://s2.loli.net/2022/02/16/Op3tR4mcxKrLTgQ.png)



## 5、set

用来更新数据库中的字段

```xml
<update id="updateEmp">
    <!-- Set标签的使用 -->
    update tbl_employee 
    <set>
        <if test="lastName!=null">
            last_name=#{lastName},
        </if>
        <if test="email!=null">
            email=#{email},
        </if>
        <if test="gender!=null">
            gender=#{gender}
        </if>
    </set>
    where id=#{id} 
    <!-- 		
            Trim：更新拼串
            update tbl_employee 
            <trim prefix="set" suffixOverrides=",">
                <if test="lastName!=null">
                    last_name=#{lastName},
                </if>
                <if test="email!=null">
                    email=#{email},
                </if>
                <if test="gender!=null">
                    gender=#{gender}
                </if>
            </trim>
            where id=#{id}  
	-->
</update>          
```



## 6、foreach 

```xml
<select id="getEmpsByConditionForeach" resultType="com.atguigu.mybatis.bean.Employee">
    select * from tbl_employee
    <!--
    collection：指定要遍历的集合：
     list类型的参数会特殊处理封装在map中，map的key就叫list
    item：将当前遍历出的元素赋值给指定的变量
    separator:每个元素之间的分隔符
    open：遍历出所有结果拼接一个开始的字符
    close:遍历出所有结果拼接一个结束的字符
    index:索引。遍历list的时候是index就是索引，item就是当前值
            遍历map的时候index表示的就是map的key，item就是map的值

    #{变量名}就能取出变量的值也就是当前遍历出的元素
     -->
    <foreach collection="ids" item="item_id" separator=","
             open="where id in(" close=")">
        #{item_id}
    </foreach>
</select>
```



mysql  foreach 批量保存的两种方式：

```xml
<!-- 第一种 -->
<!--public void addEmps(@Param("emps")List<Employee> emps);  -->
<!--MySQL下批量保存：可以foreach遍历   mysql支持values(),(),()语法-->
<insert id="addEmps">
	insert into tbl_employee(last_name,email,gender,dept_id)	
	values
	<foreach collection="emps" item="emp" separator=",">
		(#{emp.lastName},#{emp.email},#{emp.gender},#{emp.dept.id})
	</foreach>
</insert>
  
<!-- 第二种 -->
<insert id="addEmps">
    <foreach collection="emps" item="emp" separator=";">
    insert into tbl_employee(last_name,email,gender,dept_id)
    values(#{emp.lastName},#{emp.email},#{emp.gender},#{emp.dept.id})
    </foreach>
</insert>
```



## 7、内置参数_parameter&_databaseId

两个内置参数：

​	 	不只是方法传递过来的参数可以被用来判断，取值。。。

​	 	mybatis默认还有两个内置参数：

​	 	_parameter:代表整个参数

​	 		单个参数：_parameter就是这个参数

​	 		多个参数：参数会被封装为一个map；_parameter就是代表这个map

​	 	

​	 	_databaseId:如果配置了databaseIdProvider标签。

​	 		_databaseId就是代表当前数据库的别名

```xml
<select id="getEmpsTestInnerParameter" resultType="com.atguigu.mybatis.bean.Employee">
	<if test="_databaseId=='mysql'">
		select * from tbl_employee
		<if test="_parameter!=null">
			where last_name like #{lastName}
		</if>
	</if>
	<if test="_databaseId=='oracle'">
		select * from employees
		<if test="_parameter!=null">
			where last_name like #{_parameter.lastName}
		</if>
	</if>
</select>
```



## 8、bind

可以将OGNL表达式的值绑定到一个变量中，方便后来引用这个变量的值

```xml
<select id="getEmpsTestInnerParameter" resultType="com.atguigu.mybatis.bean.Employee">
	<!-- bind：可以将OGNL表达式的值绑定到一个变量中，方便后来引用这个变量的值 -->
	<bind name="_lastName" value="'%'+lastName+'%'"/>
	select * from tbl_employee
    <if test="_parameter!=null">
        where last_name like #{_lastName}
    </if>
</select>
```



## 9、可重用sql片段

定义sql片段：

```xml
<sql id="sqlColumn">
   id,last_name,email,gender
</sql>                  
```

引用sql片段：

```xml
<select id="getEmpsByConditionChoose" resultType="com.atguigu.mybatis.bean.Employee">
   select
   <include refid="sqlColumn"></include>
   from tbl_employee
   <where>
      <choose>
         <when test="id!=null">
            and id = #{id}
         </when>
         <when test="lastName!=null and lastName !=''">
            and last_name like '%${lastName}%'
         </when>
         <otherwise>
            and gender = 1
         </otherwise>
      </choose>
   </where>
</select>
```





# 五、Mybatis_缓存机制

mybatis包含一个非常强大的查询缓存特性，他可以非常方便的配置和定制，缓存可以极大的提高查询效率



mybatis系统中提供了两级缓存：

一级缓存   

二级缓存

## 1、一级缓存体验

```java
@Test
public void testFirstCache() throws IOException {
    SqlSession sqlSession = getSqlSessionFactory().openSession();

    EmployeeMapper mapper = sqlSession.getMapper(EmployeeMapper.class);
    Employee emp = mapper.getEmpById(1);
    System.out.println(emp);

    Employee emp1 = mapper.getEmpById(1);
    System.out.println(emp1);
    System.out.println(emp1==emp);
}
```

​         ![clipboard _33_.png](https://s2.loli.net/2022/02/16/iHjUKam9k8sLnQF.png)



## 2、一级缓存失效的四种情况

> 一级缓存的失效情况（没有使用到当前一级缓存的情况，也就是，还需要向数据库发出查询）      
>
> ​		1、sqlSession不同      
>
> ​		2、sqlSession相同，但是查询条件不同      
>
> ​		3、sqlSession相同，两次查询之间执行了增删改操作（这次操作可能对之前的数据有影响）      
>
> ​		4、sqlSession相同，手动清除了一级缓存              



## 3、二级缓存介绍

> 二级缓存（全局缓存） namespace级别的缓存，一个namespace对应一个二级缓存  
>
> 工作机制：  
>
> ​		1、一个会话，查询一条数据，这个数据就被放在当前会话的一级缓存中  
>
> ​		2、如果会话关闭，一级会话中的数据被保存到二级缓存中
>
> ​		3、不同namespace查询的数据会被放在自己对应的map中              



如何使用：

>  1）开启二级缓存配置 ：`<setting name="cacheEnabled" value="true"/>`      
>
> 2）去 mapper.xml 中配置二级缓存  
>
> ​		 `<cache></cache>`  
>
> 3）pojo 需要实现序列化接口              



测试：

```java
@Test
public void testSecondCache() throws IOException {
    SqlSession sqlSession1 = getSqlSessionFactory().openSession();
    SqlSession sqlSession2 = getSqlSessionFactory().openSession();

    EmployeeMapper mapper1 = sqlSession1.getMapper(EmployeeMapper.class);
    Employee emp1 = mapper1.getEmpById(1);
    System.out.println(emp1);
    sqlSession1.close();

    EmployeeMapper mapper2 = sqlSession2.getMapper(EmployeeMapper.class);
    Employee emp2 = mapper2.getEmpById(1);
    System.out.println(emp2);

    System.out.println(emp1==emp2);
}
```

![clipboard _34_.png](https://s2.loli.net/2022/02/16/64tH5yZue2fGmR3.png)



## 4、缓存有关的设置以及属性

> 和缓存有关的设置和属性      
>
> ​		1） cacheEnabled = false : 关闭二级缓存（一级缓存一直是可用的）    
>
> ​		2） 每个select标签都有一个 useCache = true       
>
>   			 //useCache = false  禁用二级缓存（对一级缓存没有影响） 
>
> ​		3） 每个增删改标签具有属性 ：flushCache =true   
>
> ​			（即执行增删改后，一级缓存就清空了，二级缓存也会被清空）    
>
>  		 	查询标签也有 flushcache 属性，只不过默认为 false   
>
> ​		4）sqlSession.clear() 只是清除当前 session 的一级缓存      
>
> ​		5）localCacheScope                



## 5、缓存原理图示

​    ![clipboard _35_.png](https://s2.loli.net/2022/02/16/neJ1D2rp7c8RxSl.png)



## 6、第三方缓存整合原理

mybatis整合ehcache作为二级缓存

1）导入ehcache的jar包和mybatis与ehcache的整合包  （引入依赖）

```xml
<dependencies>
  ...
  <dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
  </dependency>
  ...
</dependencies>
```

​        

2）在mapper.xml中配置二级缓存

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

带一些属性的二级缓存

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
    <property name="timeToIdleSeconds" value="3600"/><!--1 hour-->
    <property name="timeToLiveSeconds" value="3600"/><!--1 hour-->
    <property name="maxEntriesLocalHeap" value="1000"/>
    <property name="maxEntriesLocalDisk" value="10000000"/>
    <property name="memoryStoreEvictionPolicy" value="LRU"/>
</cache>
```



3）在类路径下添加  ehcache.xml 配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:noNamespaceSchemaLocation="../config/ehcache.xsd">
 <!-- 磁盘保存路径 -->
 <diskStore path="D:\44\ehcache" />
 
 <defaultCache 
   maxElementsInMemory="1" 
   maxElementsOnDisk="10000000"
   eternal="false" 
   overflowToDisk="true" 
   timeToIdleSeconds="120"
   timeToLiveSeconds="120" 
   diskExpiryThreadIntervalSeconds="120"
   memoryStoreEvictionPolicy="LRU">
 </defaultCache>
</ehcache>
 
<!-- 
属性说明：
diskStore：指定数据在磁盘中的存储位置。
defaultCache：当借助CacheManager.add("demoCache")创建Cache时，EhCache便会采用<defalutCache/>指定的的管理策略
 
以下属性是必须的：
maxElementsInMemory - 在内存中缓存的element的最大数目 
maxElementsOnDisk - 在磁盘上缓存的element的最大数目，若是0表示无穷大
eternal - 设定缓存的elements是否永远不过期。如果为true，则缓存的数据始终有效，如果为false那么还要根据timeToIdleSeconds，timeToLiveSeconds判断
overflowToDisk - 设定当内存缓存溢出的时候是否将过期的element缓存到磁盘上
 
以下属性是可选的：
timeToIdleSeconds - 当缓存在EhCache中的数据前后两次访问的时间超过timeToIdleSeconds的属性取值时，这些数据便会删除，默认值是0,也就是可闲置时间无穷大
timeToLiveSeconds - 缓存element的有效生命期，默认是0.,也就是element存活时间无穷大
diskSpoolBufferSizeMB 这个参数设置DiskStore(磁盘缓存)的缓存区大小.默认是30MB.每个Cache都应该有自己的一个缓冲区.
diskPersistent - 在VM重启的时候是否启用磁盘保存EhCache中的数据，默认是false。
diskExpiryThreadIntervalSeconds - 磁盘缓存的清理线程运行间隔，默认是120秒。每个120s，相应的线程会进行一次EhCache中数据的清理工作
memoryStoreEvictionPolicy - 当内存缓存达到最大，有新的element加入的时候， 移除缓存中element的策略。默认是LRU（最近最少使用），可选的有LFU（最不常使用）和FIFO（先进先出）
 -->
```





# 六、Spring整合Mybatis





# 七、Mybatis_逆向工程

## 1、Mybatis 逆向工程是什么？

> **MyBatis Generator**：简称 mbg，是一个专门为 Mybatis 框架使用者定制的代码生成器，可以快速的根据表生成对应的。
>
> 映射文件、接口和 bean 类。支持基本的增删改查，以及QBC（Query By Criteria）风格的条件查询。



## 2、如何使用

首先说一下，以下配置必须放在一个完整的 mybatis 项目下。

(即引入了mybatis相关的jar包和 具备mybatis全局配置文件）



**1）导入 mybatis 逆向工程相应的 jar 包**

​    ![clipboard _36_.png](https://s2.loli.net/2022/02/16/Xa489jx3TEMphsc.png)



**2）编写全局配置文件 mbg.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>

    <!--
        targetRuntime="MyBatis3Simple":生成简单版的CRUD
        MyBatis3:豪华版

     -->
    <context id="DB2Tables" targetRuntime="MyBatis3">
        <!-- jdbcConnection：指定如何连接到目标数据库 -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/mybatis?allowMultiQueries=true"
                        userId="root"
                        password="houchen">
        </jdbcConnection>

        <!--  -->
        <javaTypeResolver >
            <property name="forceBigDecimals" value="false" />
        </javaTypeResolver>

        <!-- javaModelGenerator：指定javaBean的生成策略
        targetPackage="test.model"：目标包名
        targetProject="\MBGTestProject\src"：目标工程
        -->
        <javaModelGenerator targetPackage="com.atguigu.mybatis.bean"
                            targetProject=".\src">
            <property name="enableSubPackages" value="true" />
            <property name="trimStrings" value="true" />
        </javaModelGenerator>

        <!-- sqlMapGenerator：sql映射生成策略： -->
        <sqlMapGenerator targetPackage="com.atguigu.mybatis.dao"
                         targetProject=".\conf">
            <property name="enableSubPackages" value="true" />
        </sqlMapGenerator>

        <!-- javaClientGenerator:指定mapper接口所在的位置 -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.atguigu.mybatis.dao"
                             targetProject=".\src">
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>

        <!-- 指定要逆向分析哪些表：根据表要创建javaBean -->
        <table tableName="tbl_dept" domainObjectName="Department"></table>
        <table tableName="tbl_employee" domainObjectName="Employee"></table>
    </context>
</generatorConfiguration>
```



**3）测试逆向工程**

```java
@Test
public void testMybatisGenerate() throws Exception {
    List<String> warnings = new ArrayList<String>();
    boolean overwrite = true;
    File configFile = new File("mbg.xml");
    ConfigurationParser cp = new ConfigurationParser(warnings);
    Configuration config = cp.parseConfiguration(configFile);
    DefaultShellCallback callback = new DefaultShellCallback(overwrite);
    MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config,
            callback, warnings);
    myBatisGenerator.generate(null);
}
```

​    

**确实生成了相应的实体、接口和 mapper：**

​    ![clipboard _37_.png](https://s2.loli.net/2022/02/16/aFA3XK2zirRwYh4.png)





# 八、mybatis_运行原理

mybatis的框架分层架构

​    ![clipboard _38_.png](https://s2.loli.net/2022/02/16/3Ja8rwFKiU5WPXY.png)

## 1、SQLSessionFactory的初始化

步骤如下

​    ![clipboard _39_.png](https://s2.loli.net/2022/02/16/ATJjVdK1NEXgcH5.png)

configuration 封装了所有的配置文件的详细信息



整个**SqlSessionFactory**的初始化总结来说：

把配置文件的信息解析并保存在**Configuration**对象中，并返回**DefaultSqlSessionFactory**对象



## 2、openSession获取SqlSession对象

​    ![0](https://note.youdao.com/yws/public/resource/268f6d5851fd1928866d1daca38c4c60/xmlnote/7939D2B17C8A4EF49C7C579FCBD78EA8/29988)



## 3、getMapper获取到接口的代理对象

​    ![clipboard _41_.png](https://s2.loli.net/2022/02/16/3xy2qIvCpbBfRuo.png)



## 4、查询实现

总结：

- 根据配置文件（全局配置，sql映射文件），初始化configuration对象

- 创建一个DefaultSqlSession对象，里面包含Configuration 以及 executor

- DefaultSqlSession.getMapper(): 拿到mapper接口对应的mapperProxy

  ​     mapperProxy中有 DefaultSqlSession

- 执行增删改查方法
  - 调用 DefaultSqlSession的增删改查
  - 创建一个StatementHangler对象，同时也会创建一个ParameterHandler 和 ResultSetHandler
  - 调用StatementHangler预编译参数和设置参数值
  - 调用StatementHangler的增删改查方法
  - 使用ResultHandler来封装结果



【注意】

​		四大对象创建的时候都有一个 interceptorChain.pluginAll(parameterHandler);





# 九、Mybatis_插件原理

## 1、插件原理

​    ![clipboard _42_.png](https://s2.loli.net/2022/02/16/lFV1za2eZjmnB87.png)

## 2、插件编写





# 十、Mybatis_扩展

## 1、分页_PageHelpler分页插件使用

1）引入分页的jar包（如果是maven工程就引入依赖）

​    ![clipboard _43_.png](https://s2.loli.net/2022/02/16/lvIpoxLZD3gCXVa.png)

2）在全局配置文件中配置分页插件

```xml
<plugins>
   <plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
</plugins>
```

3）代码中实现分页

```java
@Test
public void testMapper() throws IOException {
    SqlSession openSession = getSqlSessionFactory().openSession();
    EmployeeMapper mapper = openSession.getMapper(EmployeeMapper.class);
    //开启分页， para1:取哪一页   param2:每页多少条数据
    Page<Object> page = PageHelper.startPage(2, 2);

    List<Employee> emps = mapper.getEmps();
    for(Employee e:emps){
        System.out.println(e);
    }

    PageInfo<Employee> info = new PageInfo<>(emps);

    System.out.println("总页数："+info.getPages());
    System.out.println("总条数："+info.getTotal());
    List<Employee> list = info.getList();
    for(Employee e:list){
        System.out.println(e);
    }
}
```

​    ![clipboard _44_.png](https://s2.loli.net/2022/02/16/tzRfy8wA6Bq2eaP.png)

## 2、BatchExecutor&Spring中配置批量sqlSession

获取批量执行的sqlSession:

```java
SqlSession openSession = getSqlSessionFactory().openSession(ExecutorType.BATCH);              
```



 在与spring整合的情况下：

在spring的配置文件中，配置一个批量执行的 sqlSession









# MyBatis-Plus

文档资料：https://baomidou.com/pages/24112f/

## 代码生成器

### 1、pom引入依赖

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.1.0</version>
</dependency>
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.1.0</version>
</dependency>

<!--模板引擎-->
<dependency>
    <groupId>org.apache.velocity</groupId>
    <artifactId>velocity-engine-core</artifactId>
    <version>2.1</version>
</dependency>
```



### 2、创建代码生成配置类

