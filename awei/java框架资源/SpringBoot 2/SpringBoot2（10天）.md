---
title: SpringBoot
date: 2022-02-10 
tags:
    - SpringBoot
    - JavaEE
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

# 引言

![uTools_1644903040772.png](https://s2.loli.net/2022/02/16/HqrQ7g3iu2MZU4C.png)

中文版：

![uTools_1644903067687.png](https://s2.loli.net/2022/02/16/8UuIzK1LExgNlYn.png)

# 一、SpringBoot_简介

> 简化 Spring 应用开发的一个框架
>
> 所有 Spring 技术栈的一个大整合
>
> JavaEE 开发的一站式解决方案，人们把 Spring Boot 称为搭建程序的脚手架，它推崇约定大于配置的方式使得开发人员能够快速的构建生产级别的 spring 应用。并且尽可能的减少一切 xml 配置，做到开箱即用，迅速上手，让我们关注于业务而非配置。

## 1、SpringBoot 优点

1、快速创建独立运行的 Spring 项目以及与主流框架集成

2、使用嵌入式的 Servlet 容器，应用无需打成 war 包

3、starters 自动依赖与版本控制

4、大量的自动配置，简化开发

5、无需配置 xml，无代码生成，开箱即用

6、准生成环境，运行时应用监控

## 2、微服务

微服务：是一种架构风格

一个应用应该是一组小型服务，可以通过HTTP方式进行互通

每一个功能元素最终都是一个可独立替换和独立升级的软件单元

详细参照[微服务文档](https://martinfowler.com/articles/microservices.html#MicroservicesAndSoa)

## 3、环境准备      

环境约束

- jdk1.8：Spring Boot  推荐jdk1.7及以上；java version "1.8.0_112"；

- maven3.x：maven 3.3以上版本；Apache Maven 3.3.9；

- IntelliJ IDEA 2021.2.3；

- SpringBoot 1.5.9.RELEASE：1.5.9；



### 1）MAVEN设置

给 maven 的 settings.xml 配置文件添加 jdk 版本号和 maven阿里云 镜像

```xml
<rofile>
	<id>jdk-1.8</id>
	<activation>
		<activeByDefault>true</activeByDefault>
		<jdk>1.8</jdk>
	</activation>
<properties>
  	  <maven.compiler.source>1.8</maven.compiler.source>
		<maven.compiler.target>1.8</maven.compiler.target>
		<maven.compilen.compilerVersion>1.8</maven.compiler.compilenVension>
	</properties>
</profile>

<!--阿里云maven镜像仓库-->
<mirrors>
	<mirror>
		<id>nexus-aliyun</id>
		<mirrorOf>*</mirrorOf>
		<name>Nexus aliyun</name>
		<url>http://maven.aliyun.com/nexus/content/groups/public</url>
	</mirror> 
</mirrors>
```



## 4、HelloWorld 程序

### 第一步：创建一个 maven 工程

### 第二步：导入SpringBoot的相关依赖

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.9.RELEASE</version>
</parent>                                                                                                                                
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

### 第三步：编写主程序，启动项目

```java
/**
 *  @SpringBootApplication 来标注一个主程序类，说明这是一个Spring Boot应用
 */
@SpringBootApplication
public class HelloWorldMainApplication {
    public static void main(String[] args) {
        // SpringBoot 应用启动起来
        SpringApplication.run(HelloWorldMainApplication.class,args);
    }
```

### 第四步：编写 业务逻辑 Controller、Service

```java
//@Controller
//@ResponseBody
@RestController
public class HelloController {

    //@ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World!";
    }
}
```

### 第五步：运行主程序测试

### 第六步：简化部署

```xml
<!-- 这个插件，可以将应用打包成一个可执行的jar包 -->
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

将这个应用达成jar包,直接使用java -jar的命令执行

![uTools_1644939745969.png](https://s2.loli.net/2022/02/16/xqkjBmedz6XIYJ3.png)



## 5、HelloWorld 原理说明

### 1、pom文件

#### 1）父工程

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.9.RELEASE</version>
</parent>

他的父项目是：
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-dependencies</artifactId>
  <version>1.5.9.RELEASE</version>
  <relativePath>../../spring-boot-dependencies</relativePath>
</parent>
他来真正管理Spring Boot应用里面的所有依赖版本；
```

这称为 Spring Boot的版本仲裁中心

以后我们导入依赖时不需要写版本号；（没有在 dependencies 管理的依赖自然要写jar包）

#### 2）启动器

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

**spring-boot-starter-web：**

> **spring-boot-starter是 spring-boot的场景启动器**；帮我们导入了web模块正常运行所依赖的组件；
>
> spring boot 将所有的功能场景都抽取出来，做成一个个的starters（启动器），只需要在项目里面引入这些starter,那么相关场景的所有依赖都会导入进来。要用什么功能，就导入什么场景的启动器即可。



### 2、主程序类（主入口类）

```java
/**
 *  @SpringBootApplication 来标注一个主程序类，说明这是一个Spring Boot应用
 */
@SpringBootApplication
public class HelloWorldMainApplication {
    public static void main(String[] args) {
        // Spring应用启动起来
        SpringApplication.run(HelloWorldMainApplication.class,args);
    }
}
```

- **@SpringBootApplication** ： SpringBoot应用标志在某个类上，说明这个类是 SpringBoot 项目的主配置类，SpringBoot 应该运行这个类的main方法来启动SpringBoot项目 ；

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
      @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
      @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
```

- **@SpringBootConfiguration** ：标志在某个类上，标志着这是一个 SpringBoot的配置类

- **@Configuration** ：配置类上来标识这个注解；

  配置类 === 配置文件 ；配置类也是容器中的一个组件 @Component

- **@EnableAutoConfiguration**：**开启自动配置功能**

  以前我们需要配置的东西，Spring Boot会帮助我们自动配置；@**EnableAutoConfiguration** 告诉 SpringBoot 开启自动配置功能，这样自动配置才能生效

```java
@AutoConfigurationPackage 
@Import({AutoConfigurationImportSelector.class}) 
public @interface EnableAutoConfiguration {          
```

- **@AutoConfigurationPackage**：**自动配置包**

- @**Import**(AutoConfigurationPackages.Registrar.class)：

 Spring 的底层注解 @import，给容器中导入一个组件：导入的组件由 AutoConfigurationPackages.Registrar.class 指定；

**将主配置类（@SpringBootApplication标注的类）所在包及下面的所有子包里面的所有组件扫描到 Spring 容器；**

- **@Import(EnableAutoConfigurationImportSelector.class)**



#### 如何给容器中导入组件？

 **EnableAutoConfigurationImportSelector**：导入哪些组件的选择器；

 将所有需要导入的组件以全类名的方式返回；这些组件就会被添加到容器中；

 会给容器中导入非常多的自动配置类（xxxAutoConfiguration）；就是给容器中导入这个场景需要的所有组件，并配置好这些组件；
![20190105173817619.png](https://s2.loli.net/2022/02/16/zHKMaphXidtjlUs.png)



有了自动配置类，免去了我们手动编写配置注入功能组件等的工作；

`SpringFactoriesLoader.loadFactoryNames(EnableAutoConfiguration.class,classLoader)；`

SpringBoot在启动的时候从类路径下的 `META-INF/spring.factorie`s 中获取 `EnableAutoConfiguration` 指定的值，将这些值作为自动配置类导入到容器中，自动配置类就生效，帮我们进行自动配置工作；以前我们需要自己配置的东西，自动配置类都帮我们；

JavaEE的整体整合解决方案和自动配置都在 `spring-boot-autoconfigure-1.5.9.RELEASE.jar`；



## 6、开发小技巧

### 1）Lombok

```xml
<groupId>org.projectlombok</groupId>
<artifactId>lombok</artifactId>
```

- **@Data** 	 getter/setter 方法
- **@ToString**       toString() 方法
- **@AllArgsConstructor**  有参构造
- **@NoAegsConstructor**  无参构造



### 2）dev-tools

```xml
<groupId>org.spingframework.boot</groupId>
<artifactId>spring-boot-devtools</artifactId>
<optional>true</optional>
```

**Ctrl + F9** 把项目重新编译，`devtoos` 会自动帮我们把项目重新部署。



### 3）Spring Initailizr

一键打包初始化项目。IDEA中可以直接在项目中创建 Spring Initailizr 项目，然后根据你所需要的场景进行选择，之后生成的项目会自动帮我们初始化好我们所需要的东西（项目结构、依赖等）。





# 二、SpringBoot_配置

## 1、配置文件

Spring Boo t使用一个全局的配置文件，配置文件的名称是固定的

- **application.properties**

- **application.yml**

1）**配置文件的作用： 修改 SpringBoot 自动配置的默认值**

> YAML（YAML Ain't Markup Language）
>
> YAML A  Markup Language：是一个标记语言
>
> YAML  isn't  Markup Language：不是一个标记语言

2）**标记语言：**

> 以前的配置文件，大多是 xxx.xml 文件
>
> YAML： 以数据为中心，比 json、xml 更适合作配置文件。

3）**配置例子：**

 YAML：

```yaml
server:
	port:8081
```

xml：

```xml
<server>
	<port>8081</port>
</server>
```



## 2、YAML 配置文件

菜鸟教程：https://www.runoob.com/w3cnote/yaml-intro.html

### 1）基本语法

k: v    ==>  表示一个键值对

以空格的缩进来控制层级关系；只要左对齐的一列数据，都是同一层级的

```yaml
server:  
	port: 8081             
	path: /hello 
```

注：属性和值都是大小写敏感的

### 2）值的写法

- **字面量：普通的值（数字、字符串，布尔）**

k: v  ==> 字面量直接来写

字符串默认不用加上双引号或者单引号;

“ ”：（双引号）

name: "zhangsan \n lisi"  ==> 输出： zhangsan 换行 lisi

' ' ：（单引号）

name: "zhangsan \n lisi"   ==> 输出：zhangsan \n lisi

- **对象、map**

k: v ==>  在下一行来写对象的属性和值的关系

friends:    lastName: zhangsan    age: 20              

 	行内写法：friends: {lastName: zhangsan,age: 20}      

- **数组（List,Set):**

用 **- 值** 来表示数组中的一个元素

 	pets:    
 		- cat    
 		- dog    
 		- pig              
 	
 	行内写法：
 	pets: [cat,dog,pig]



## 3、配置文件值注入

**1、@Value 和 @ConfigurationProperties 为属性注入值对比**

![clipboard.png](https://s2.loli.net/2022/02/16/IM3q4jonuEz2y5x.png)

配置文件 yml 和 properties 都能获取到值



**2、什么时候使用 @ConfigurationProperties 和 @Value?** 

- 如果说，我们需要在某个业务逻辑中**获取**一下**配置文件中的某项值**，使用 **@Value**

- 如果说，我们专门编写了一个 **JavaBean 来进行配置文件的映射，**则应该使用 **@ConfigurationProperties**

注：@Value 不支持复杂的属性注入



**3、配置文件注入值数据校验**

```java
@Component
@ConfigurationProperties(prefix = "person")
@Validated
public class Person {

    /**
     * <bean class="Person">
     *      <property name="lastName" value="字面量/${key}从环境变量、配置文件中获取值/#{SpEL}"></property>
     * <bean/>
     */

   //lastName必须是邮箱格式
    @Email
    //@Value("${person.last-name}")
    private String lastName;
    //@Value("#{11*2}")
    private Integer age;
    //@Value("true")
    private Boolean boss;

    private Date birth;
    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
    }
```

**3、@PropertiesSource & @ImportResource & @Bean**

- **@PropertiesSource** :  将该注解放在相应的配置类上   ==》  加载指定的配置文件。

  ```java
  /**
   * 将配置文件中配置的每一个属性的值，映射到这个组件中
   * @ConfigurationProperties：告诉SpringBoot将本类中的所有属性和配置文件中相关的配置进行绑定；
   *      prefix = "person"：配置文件中哪个下面的所有属性进行一一映射
   *
   * 只有这个组件是容器中的组件，才能容器提供的@ConfigurationProperties功能；
   *  @ConfigurationProperties(prefix = "person")默认从全局配置文件中获取值；
   *
   */
  @PropertySource(value = {"classpath:person.properties"})
  @Component
  @ConfigurationProperties(prefix = "person")
  //@Validated
  public class Person {
  
      /**
       * <bean class="Person">
       *      <property name="lastName" value="字面量/${key}从环境变量、配置文件中获取值/#{SpEL}"></property>
       * <bean/>
       */
  
     //lastName必须是邮箱格式
     // @Email
      //@Value("${person.last-name}")
      private String lastName;
      //@Value("#{11*2}")
      private Integer age;
      //@Value("true")
      private Boolean boss;
  }
  ```

- **@ImportResource** : 导入Spring的配置文件   ===》 让配置文件里面的内容生效。

SpringBoot 里面没有 Spring 的配置文件，我们自己编写的配置文件，也不能自动识别；想要 Spring 的配置文件生效，需要使用 @ImportResource 将其加载进来；

@ImportResource 标注在一个配置类上	 `@ImportResource(locations = {"classpath:beans.xml"})`              

不来编写Spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="helloService" class="com.superbeyone.springboot.service.HelloService"></bean>
</beans>
```

- **@Bean**：标注在配置类的方法上面  ===》 给容器中添加组件。

spring boot 推荐使用全注解的方式 向容器中添加组件

1）编写配置类  ===》相当于 Spring 的配置文件

2）使用 @Bean 向容器中添加组件

```java
/**
 * @Configuration : 指明当前类就是一个配置类，代替原来的 Spring 配置文件
 */
@Configuration
public class MyAppConfig {

    @Bean   //将方法的返回值添加到容器中，容器中这个组件默认的id就是方法名
    public HelloService helloService(){
        System.out.println("配置类@Bean给容器中添加组件了...");
        return  new HelloService();
    }
}
```



## 4、配置文件占位符

**1、随机数**         

```properties
${random.value}
${random.int}
${random.long}
```

**2、占位符获取之前配置的值，如果没有可以使用  ：指定默认值**

```properties
person.last-name=zhangsan
person.age=19
person.boss=false
person.dog.name = ${person.last-name:zhaoliu}_dog
```



## 5、Profile

参考文档：https://www.cnblogs.com/elnimo/p/13779443.html

**1、多 profile 文件**

我们在编写主配置文件时，文件名可以是 `applicaton-{profile}.properties/yml`

**默认使用 `application.properties`**

激活指定的配置 ： 在 **`application.properties`** 中指定 `spring.profiles.active=dev`

**2、yml 的文档块方式**

```yaml
server:
  port: 8081
spring:
  profiles:
    active: dev
---
server:
  port: 8083

spring:
  profiles: dev

---
server:
  port: 8084
spring:
  profiles: prod
```

​           

**3、激活指定的profile**

1） 在配置文件中指定  `spring.profiles.active = dev`

2）以命令行的方式启动

​	`-spring.profiles.active = dev` 

3）虚拟机参数

`-Dspring.profiles.active = dev`



## 6、配置文件的加载顺序

springboot 会扫描以下位置的的 `application.properties / application.yml` 作为spring boot 的配置文件

**-file:  ./config/**

**-file :  ./**

**-classpath :  /config/**

**-classpath :  /**

优先级由高到低，高优先级的配置会覆盖低优先级的配置

springboot 会从这四个位置全部加载主配置文件，**多个文件之间会形成互补配置**

**我们还可以通过 `spring.config.location` 来改变默认的配置文件位置**

项目打包好以后，我们在启动项目时，可以通过命令行参数的形式来指定配置文件的新位置

指定的配置文件和默认加载的配置文件共同起作用形成互补配置

`java -jar spring-boot-01-helloworld-1.0-SNAPSHOT.jar`   `--spring.config.location = 配置文件的绝对路径`



## 7、外部配置的加载顺序

**springboot 可以从以下位置加载配置，优先级从高到低；高优先级的配置覆盖低优先级的配置，所有的配置会形成互补配置。**

1）命令行参数

- 所有的配置都可以在命令行上进行指定 `java -jar spring-boot-02-config-02-0.0.1-SNAPSHOT.jar --server.port=8087 --server.context-path=/abc`	

- 多个配置用空格分开； --配置项=值

2）来自 `java:comp/env` 的 `JNDI` 属性

3）Java 系统属性`（System.getProperties()）`

4）操作系统环境变量

5）`RandomValuePropertySource` 配置的 `random.*` 属性值

- 由 jar 包外向 jar 包内进行寻找
- 优先加载 带 profile

6）jar 包外部的 `application-{profile}.properties` 或 `application-{profile}.yml` 配置文件

7）jar 包内部的 `application-{profile}.properties` 或 `application-{profile}.yml` 配置文件

- 再来加载不带 profile

8）jar 包外部的 `application.propertie`s 或 `application.yml` 配置文件

9）jar 包内部的 `application.properties` 或 `application.yml` 配置文件

10）@Configuration 注解类上的 @PropertySource

11）通过 `SpringApplication.setDefaultProperties` 指定的默认属性



## 8、自动配置原理

根据源码分析。





# 三、SpringBoot_日志

## 1、日志框架

**市面上的日志框架**

JUL、JCL、Jboss-logging 、logback 、log4j、 log4j4等。

|                  日志门面 （日志的抽象层）                   |                       日志实现                        |
| :----------------------------------------------------------: | :---------------------------------------------------: |
| JCL（Jakarta Commons Logging） SLF4j（Simple Logging Facade for Java） **jboss-logging** | Log4j 、JUL（java.util.logging）、Log4j2、**Logback** |

左边选一个日志门面（抽象层），右边来选一个实现

日志门面：SLF4j（有一个注解 @slf4j，可以打印信息）

日志实现：Logback

SpringBoot ：底层是 Spring 框架，Spring 默认选用的是  JCL

Spring：默认选用的是 SLF4j 和 Logback



## 2、SLF4j 的使用

### 1）如何在系统中使用SLF4j

开发的时候，日志记录方法的调用，不应该直接调用日志的实现类，而是调用日志抽象层里面的方法

给系统里面导入 slf4j 的 jar 和 logback 的实现 jar

```java
import org.slf4j.Logger; 
import org.slf4j.LoggerFactory; 
public class HelloWorld { 
    public static void main(String[] args) { 
        Logger logger = LoggerFactory.getLogger(HelloWorld.class);  
        logger.info("Hello World");  
    } 
}        
```

![1592357498_1_.png](https://s2.loli.net/2022/02/16/6N7Q2R413jmtXpv.png)

**每一个日志的框架都有自己的配置文件，使用slf4j以后**，配置文件还是做成日志实现框架本身的

**配置文件**

### 2）遗留问题

假如一个系统使用的日志框架为 slf4j和logback ，并且这个系统还使用了spring（commons-logging)、mybatis 等框架，每个框架内置的日志框架是不一样的

===》统一日志记录，即使是别的框架

![clipboard _1_.png](https://s2.loli.net/2022/02/16/piQuJwmFf831IdK.png)

**如何让系统中的所有日志都统一到slf4j**

**1、将系统中的其他日志框架先排除出去**

**2、用中间包来替换原有的日志框架**

**3、导入slf4j的其他实现**

**3、SpringBoot 日志关系**

![1592359310_1_.png](https://s2.loli.net/2022/02/16/hYHSDz7UQdNCZa6.png)

总结：

1）、SpringBoot也是使用slf4j+logback的方式进行日志记录

2）、SpringBoot也把其他的日志都替换成slf4j

3）、中间替换包

**4）、如果我们引入了其他框架，一定要把这个框架的默认日志移除**

Spring框架用的是commons-logging；

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <exclusions>
        <exclusion>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

**springboot能够自动适配所有的日志，而且底层使用slf4j+logback的方式记录日志，引入其他框架时，需要把这个框架依赖的日志框架排除**

## 4、日志的使用

### 1）默认配置

SpringBoot默认帮我们配置好了日志；

```java
//记录器
Logger logger = LoggerFactory.getLogger(getClass());
@Test
public void contextLoads() {
    //System.out.println();

    //日志的级别；
    //由低到高   trace<debug<info<warn<error
    //可以调整输出的日志级别；日志就只会在这个级别以以后的高级别生效
    logger.trace("这是trace日志...");
    logger.debug("这是debug日志...");
    //SpringBoot默认给我们使用的是info级别的，没有指定级别的就用				SpringBoot默认规定的级别；root级别
    logger.info("这是info日志...");
    logger.warn("这是warn日志...");
    logger.error("这是error日志...");
}
```

```
日志输出格式：
        %d表示日期时间，
        %thread表示线程名，
        %-5level：级别从左显示5个字符宽度
        %logger{50} 表示logger名字最长50个字符，否则按照句点分割。 
        %msg：日志消息，
        %n是换行符
    -->
    %d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n
```

SpringBoot修改日志的默认配置

```
logging.level.com.superbeyone=trace


#logging.path=
# 不指定路径在当前项目下生成 springboot.log 日志
# 可以指定完整的路径；
#logging.file=G:/springboot.log

# 在当前磁盘的根路径下创建spring文件夹和里面的log文件夹；使用 spring.log 作为默认文件
logging.path=/spring/log

#  在控制台输出的日志的格式
logging.pattern.console=%d{yyyy-MM-dd} [%thread] %-5level %logger{50} - %msg%n
# 指定文件中日志输出的格式
logging.pattern.file=%d{yyyy-MM-dd} === [%thread] === %-5level === %logger{50} ==== %msg%n
```

| logging.file | logging.path | Example  | Description                        |
| ------------ | ------------ | -------- | ---------------------------------- |
| (none)       | (none)       |          | 只在控制台输出                     |
| 指定文件名   | (none)       | my.log   | 输出日志到 my.log 文件             |
| (none)       | 指定目录     | /var/log | 输出到指定目录的 spring.log 文件中 |



### 2）指定配置

给类路径下放上每个日志框架自己的配置文件即可；SpringBoot就不使用他默认配置的了

| Logging System          | Customization                                                |
| ----------------------- | ------------------------------------------------------------ |
| Logback                 | logback-spring.xml, logback-spring.groovy, logback.xml or logback.groovy |
| Log4j2                  | log4j2-spring.xml or log4j2.xml                              |
| JDK (Java Util Logging) | logging.properties                                           |

**logback.xml**：直接就被日志框架识别了；

**logback-spring.xml**：日志框架就不直接加载日志的配置项，由SpringBoot解析日志配置，可以使用SpringBoot的高级 Profile 功能

```xml
<springProfile name="staging">
    <!-- configuration to be enabled when the "staging" profile is active -->
    可以指定某段配置只在某个环境下生效
</springProfile>
```

如：

```xml
<appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
        <!--
        日志输出格式：
            %d表示日期时间，
            %thread表示线程名，
            %-5level：级别从左显示5个字符宽度
            %logger{50} 表示logger名字最长50个字符，否则按照句点分割。 
            %msg：日志消息，
            %n是换行符
        -->
        <layout class="ch.qos.logback.classic.PatternLayout">
            <springProfile name="dev">
                <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} ----> [%thread] ---> %-5level %logger{50} - %msg%n</pattern>
            </springProfile>
            <springProfile name="!dev">
                <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} ==== [%thread] ==== %-5level %logger{50} - %msg%n</pattern>
            </springProfile>
        </layout>
    </appender>
```



## 5、切换日志框架

可以按照slf4j的日志适配图，进行相关的切换；

**slf4j + log4j的方式：**

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
  <exclusions>
    <exclusion>
      <artifactId>logback-classic</artifactId>
      <groupId>ch.qos.logback</groupId>
    </exclusion>
    <exclusion>
      <artifactId>log4j-over-slf4j</artifactId>
      <groupId>org.slf4j</groupId>
    </exclusion>
  </exclusions>
</dependency>

<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-log4j12</artifactId>
</dependency>
```



**切换为log4j2**

```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>spring-boot-starter-logging</artifactId>
                    <groupId>org.springframework.boot</groupId>
                </exclusion>
            </exclusions>
        </dependency>

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-log4j2</artifactId>
</dependency>
```





# 四、SpringBoot_Web开发

## 1、简介

**使用 SpringBoot：**

- 创建 SpringBoot 应用，选中我们需要的模块

- SpringBoot 已经默认将这些场景配置好了，只需要在配置文件中指定少量的配置就可以运行起来

- 自己编写业务代码

### 自动配置原理？

> 这个场景SpringBoot帮我们配置了什么？能不能修改？可以修改哪些？能不能扩展？
>
> xxxxAutoConfiguration：帮我们给容器中自动配置组件； 
>
> xxxxProperties:配置类来封装配置文件的内容；              



## 2、SpringBoot对静态资源的映射规则

```java
@ConfigurationProperties(prefix = "spring.resources", ignoreUnknownFields = false)
public class ResourceProperties implements ResourceLoaderAware {
  //可以设置和静态资源有关的参数，缓存时间等
```

```java
 WebMvcAuotConfiguration：
        @Override
        public void addResourceHandlers(ResourceHandlerRegistry registry) {
            if (!this.resourceProperties.isAddMappings()) {
                logger.debug("Default resource handling disabled");
                return;
            }
            Integer cachePeriod = this.resourceProperties.getCachePeriod();
            if (!registry.hasMappingForPattern("/webjars/**")) {
                customizeResourceHandlerRegistration(
                        registry.addResourceHandler("/webjars/**")
                                .addResourceLocations(
                                        "classpath:/META-INF/resources/webjars/")
                        .setCachePeriod(cachePeriod));
            }
            String staticPathPattern = this.mvcProperties.getStaticPathPattern();
            //静态资源文件夹映射
            if (!registry.hasMappingForPattern(staticPathPattern)) {
                customizeResourceHandlerRegistration(
                        registry.addResourceHandler(staticPathPattern)
                                .addResourceLocations(
                                        this.resourceProperties.getStaticLocations())
                        .setCachePeriod(cachePeriod));
            }
        }

        //配置欢迎页映射
        @Bean
        public WelcomePageHandlerMapping welcomePageHandlerMapping(
                ResourceProperties resourceProperties) {
            return new WelcomePageHandlerMapping(resourceProperties.getWelcomePage(),
                    this.mvcProperties.getStaticPathPattern());
        }

       //配置喜欢的图标
        @Configuration
        @ConditionalOnProperty(value = "spring.mvc.favicon.enabled", matchIfMissing = true)
        public static class FaviconConfiguration {

            private final ResourceProperties resourceProperties;

            public FaviconConfiguration(ResourceProperties resourceProperties) {
                this.resourceProperties = resourceProperties;
            }

            @Bean
            public SimpleUrlHandlerMapping faviconHandlerMapping() {
                SimpleUrlHandlerMapping mapping = new SimpleUrlHandlerMapping();
                mapping.setOrder(Ordered.HIGHEST_PRECEDENCE + 1);
                //所有  **/favicon.ico 
                mapping.setUrlMap(Collections.singletonMap("**/favicon.ico",
                        faviconRequestHandler()));
                return mapping;
            }

            @Bean
            public ResourceHttpRequestHandler faviconRequestHandler() {
                ResourceHttpRequestHandler requestHandler = new ResourceHttpRequestHandler();
                requestHandler
                        .setLocations(this.resourceProperties.getFaviconLocations());
                return requestHandler;
            }

        }
```

**1）所有的  /webjars/, 都去 classpath:/META-INF/resources/webjars/ 找资源****

  **webjars：以 jar 包的方式引入静态资源；**

 ![clipboard _2_.png](https://s2.loli.net/2022/02/16/uVGkNY1WyZmw6SD.png)



**2）/  访问当前项目的任何资源，都去（静态资源的文件夹）下寻找**

 `"classpath:/META-INF/resources/",  "classpath:/resources/", "classpath:/static/",  "classpath:/public/"  "/"：当前项目的根路径`              

![clipboard _3_.png](https://s2.loli.net/2022/02/16/ZbsUPM12HDRpxmI.png)

**3）欢迎页： 静态资源文件夹下的所有 index.html 页面**

​	localhost:8080/   找index页面

**4）所有的 `**/favicon.ico`  都是在静态资源文件下找**

![clipboard _4_.png](https://s2.loli.net/2022/02/16/PAwLRQsfeaqr6KU.png)



## 3、模板引擎 thymeleaf

> SpringBoot推荐的Thymeleaf；
>
> 语法更简单，功能更强大；

![clipboard _5_.png](https://s2.loli.net/2022/02/16/HqrhXlAWejysbgu.png)

### 1）引入 thymeleaf

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
    2.1.6
</dependency>
切换thymeleaf版本
<properties>
    <thymeleaf.version>3.0.9.RELEASE</thymeleaf.version>
    <!-- 布局功能的支持程序  thymeleaf3主程序  layout2以上版本 -->
    <!-- thymeleaf2   layout1-->
    <thymeleaf-layout-dialect.version>2.2.2</thymeleaf-layout-dialect.version>
</properties>
```



### 2）thymeleaf的语法

```java
@ConfigurationProperties(prefix = "spring.thymeleaf")
public class ThymeleafProperties {

    private static final Charset DEFAULT_ENCODING = Charset.forName("UTF-8");

    private static final MimeType DEFAULT_CONTENT_TYPE = MimeType.valueOf("text/html");

    public static final String DEFAULT_PREFIX = "classpath:/templates/";

    public static final String DEFAULT_SUFFIX = ".html";

```



**只要我们把HTML页面放在 classpath:/templates/ , thymeleaf就能自动渲染**

使用步骤：

1、导入thymeleaf的名称空间

2、使用thymeleaf语法；

![clipboard _6_.png](https://s2.loli.net/2022/02/16/EOScQDeqh2wBmY1.png)



### 3）如何使用thymeleaf

**1、导入thymeleaf的名称空间 ==》使页面具备语法提示**

```html
<html lang="en" xmlns:th="http://www.thymeleaf.org">              
```

**2、使用thymeleaf语法；**

- th:text  改变当前元素里面文本内容的值

- th:任意html属性  替换 html 原生属性的值

更多的属性：

![clipboard _7_.png](https://s2.loli.net/2022/02/16/WFftOl9QropxajD.png)

**2）thymeleaf表达式**

```yaml
Simple expressions:（表达式语法）
    Variable Expressions: ${...}：获取变量值；OGNL；
            1）、获取对象的属性、调用方法
            2）、使用内置的基本对象：
                #ctx : the context object.
                #vars: the context variables.
                #locale : the context locale.
                #request : (only in Web Contexts) the HttpServletRequest object.
                #response : (only in Web Contexts) the HttpServletResponse object.
                #session : (only in Web Contexts) the HttpSession object.
                #servletContext : (only in Web Contexts) the ServletContext object.
                
                ${session.foo}
            3）、内置的一些工具对象：
#execInfo : information about the template being processed.
#messages : methods for obtaining externalized messages inside variables expressions, in the same way as they would be obtained using #{…} syntax.
#uris : methods for escaping parts of URLs/URIs
#conversions : methods for executing the configured conversion service (if any).
#dates : methods for java.util.Date objects: formatting, component extraction, etc.
#calendars : analogous to #dates , but for java.util.Calendar objects.
#numbers : methods for formatting numeric objects.
#strings : methods for String objects: contains, startsWith, prepending/appending, etc.
#objects : methods for objects in general.
#bools : methods for boolean evaluation.
#arrays : methods for arrays.
#lists : methods for lists.
#sets : methods for sets.
#maps : methods for maps.
#aggregates : methods for creating aggregates on arrays or collections.
#ids : methods for dealing with id attributes that might be repeated (for example, as a result of an iteration).

    Selection Variable Expressions: *{...}：选择表达式：和${}在功能上是一样；
        补充：配合 th:object="${session.user}：
   <div th:object="${session.user}">
    <p>Name: <span th:text="*{firstName}">Sebastian</span>.</p>
    <p>Surname: <span th:text="*{lastName}">Pepper</span>.</p>
    <p>Nationality: <span th:text="*{nationality}">Saturn</span>.</p>
    </div>
    
    Message Expressions: #{...}：获取国际化内容
    Link URL Expressions: @{...}：定义URL；
            @{/order/process(execId=${execId},execType='FAST')}
    Fragment Expressions: ~{...}：片段引用表达式
            <div th:insert="~{commons :: main}">...</div>
            
Literals（字面量）
      Text literals: 'one text' , 'Another one!' ,…
      Number literals: 0 , 34 , 3.0 , 12.3 ,…
      Boolean literals: true , false
      Null literal: null
      Literal tokens: one , sometext , main ,…
Text operations:（文本操作）
    String concatenation: +
    Literal substitutions: |The name is ${name}|
Arithmetic operations:（数学运算）
    Binary operators: + , - , * , / , %
    Minus sign (unary operator): -
Boolean operations:（布尔运算）
    Binary operators: and , or
    Boolean negation (unary operator): ! , not
Comparisons and equality:（比较运算）
    Comparators: > , < , >= , <= ( gt , lt , ge , le )
    Equality operators: == , != ( eq , ne )
Conditional operators:条件运算（三元运算符）
    If-then: (if) ? (then)
    If-then-else: (if) ? (then) : (else)
    Default: (value) ?: (defaultvalue)
Special tokens:
    No-Operation: _ 
```



## 4、SpringMVC 自动配置

文档资料：https://docs.spring.io/spring-boot/docs/1.5.10.RELEASE/reference/htmlsingle/#boot-features-developing-web-applications

### 1）auto-configuration

Spring Boot 自动配置好了SpringMVC

以下是 SpringBoot 对 SpringMVC 的默认配置:**（WebMvcAutoConfiguration）**

- Inclusion of ContentNegotiatingViewResolver and BeanNameViewResolver beans.
  - 自动配置了ViewResolver（视图解析器：根据方法的返回值得到视图对象（View），视图对象决定如何渲染（转发？重定向？））
  - ContentNegotiatingViewResolver：组合所有的视图解析器的；
  - 如何定制：我们可以自己给容器中添加一个视图解析器；自动的将其组合进来；
- Support for serving static resources, including support for WebJars (see below).静态资源文件夹路径,webjars

- Static index.html support. 静态首页访问

- Custom Favicon support (see below). favicon.ico

- 自动注册了 of Converter, GenericConverter, Formatter beans.

  - Converter：转换器； public String hello(User user)：类型转换使用Converter

  - Formatter 格式化器； 2017.12.17===Date； 

    ```java
    @Bean
    @ConditionalOnProperty(prefix = "spring.mvc", name = "date-format")//在文件中配置日期格式化的规则
    public Formatter<Date> dateFormatter() {
        return new DateFormatter(this.mvcProperties.getDateFormat());//日期格式化组件
    }
    ```

自己添加的格式化器转换器，我们只需要放在容器中即可

- Support for HttpMessageConverters (see below).

  - HttpMessageConverter：SpringMVC用来转换Http请求和响应的；User—Json；

  - HttpMessageConverters 是从容器中确定；获取所有的HttpMessageConverter；

    自己给容器中添加HttpMessageConverter，只需要将自己的组件注册容器中（@Bean,@Component）

- Automatic registration of MessageCodesResolver (see below).定义错误代码生成规则

- Automatic use of a ConfigurableWebBindingInitializer bean (see below).

我们可以配置一个ConfigurableWebBindingInitializer来替换默认的；（添加到容器）

```
初始化WebDataBinder；
请求数据=====JavaBean；
```

> **org.springframework.boot.autoconfigure.web：web的所有自动场景；**
>
> If you want to keep Spring Boot MVC features, and you just want to add additional MVC configuration (interceptors, formatters, view controllers etc.) you can add your own @Configuration class of type WebMvcConfigurerAdapter, but without @EnableWebMvc. If you wish to provide custom instances of RequestMappingHandlerMapping, RequestMappingHandlerAdapter or ExceptionHandlerExceptionResolver you can declare a WebMvcRegistrationsAdapter instance providing such components.
>
> If you want to take complete control of Spring MVC, you can add your own @Configuration annotated with @EnableWebMvc.



### 2）扩展SpringMVC

```xml
<mvc:view-controller path="/hello" view-name="success"/>
<mvc:interceptors>
    <mvc:interceptor>
        <mvc:mapping path="/hello"/>
        <bean></bean>
    </mvc:interceptor>
</mvc:interceptors>
```

a>**编写一个配置类（@Configuration），是 WebMvcConfigurerAdapter 类型；不能标注 @EnableWebMvc**

既保留了所有的自动配置，也能用我们扩展的配置；

```java
//使用 WebMvcConfigurerAdapter 可以来扩展 SpringMVC 的功能
@Configuration
public class MyMvcConfig extends WebMvcConfigurerAdapter {

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        // super.addViewControllers(registry);
        //浏览器发送 /superbeyone 请求来到 success
        registry.addViewController("/superbeyone").setViewName("success");
    }
}
```

**b>原理：**

 1）**WebMvcAutoConfiguration 是 SpringMVC 的自动配置类**

 2）在做其他自动配置时会导入 `@Import(EnableWebMvcConfiguration.class)`

```java
@Configuration
public static class EnableWebMvcConfiguration extends DelegatingWebMvcConfiguration {
    private final WebMvcConfigurerComposite configurers = new WebMvcConfigurerComposite();

    //从容器中获取所有的WebMvcConfigurer
    @Autowired(required = false)
    public void setConfigurers(List<WebMvcConfigurer> configurers) {
        if (!CollectionUtils.isEmpty(configurers)) {
            this.configurers.addWebMvcConfigurers(configurers);
            //一个参考实现；将所有的WebMvcConfigurer相关配置都来一起调用；  
            @Override
            // public void addViewControllers(ViewControllerRegistry registry) {
            //    for (WebMvcConfigurer delegate : this.delegates) {
            //       delegate.addViewControllers(registry);
            //   }
        }
    }
}
```

 3）容器中所有的 WebMvcConfigurer 都会一起起作用；

 4）我们的配置类也会被调用；

 **效果：SpringMVC的自动配置和我们的扩展配置都会起作用；**



### 3）全面接管SpringMVC；

SpringBoot对SpringMVC的自动配置不需要了，所有都是我们自己配置；所有的SpringMVC的自动配置都失效了

a>**我们需要在配置类中添加 @EnableWebMvc 即可；**

```java
//使用WebMvcConfigurerAdapter可以来扩展SpringMVC的功能
@EnableWebMvc
@Configuration
public class MyMvcConfig extends WebMvcConfigurerAdapter {

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        // super.addViewControllers(registry);
        //浏览器发送 /superbeyone 请求来到 success
        registry.addViewController("/superbeyone").setViewName("success");
    }
}
```

b>**原理：**

为什么 **@EnableWebMvc** 自动配置就失效了；

1）**@EnableWebMvc** 的核心

```java
@Import(DelegatingWebMvcConfiguration.class)
public @interface EnableWebMvc {
```


2）

```java
@Configuration
public class DelegatingWebMvcConfiguration extends WebMvcConfigurationSupport {
```


3）

```java
@Configuration
@ConditionalOnWebApplication
@ConditionalOnClass({ Servlet.class, DispatcherServlet.class,
        WebMvcConfigurerAdapter.class })
//容器中没有这个组件的时候，这个自动配置类才生效
@ConditionalOnMissingBean(WebMvcConfigurationSupport.class)
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE + 10)
@AutoConfigureAfter({ DispatcherServletAutoConfiguration.class,
        ValidationAutoConfiguration.class })
public class WebMvcAutoConfiguration {
```

4）**@EnableWebMvc** 将 **WebMvcConfigurationSupport** 组件导入进来；

5）导入的 **WebMvcConfigurationSupport** 只是 **SpringMVC** 最基本的功能；


## 5、如何修改SpringBoot的默认配置

**模式：**

1）**SpringBoot** 在自动配置很多组件的时候，先看容器中有没有用户自己配置的（**@Bean、@Component**）如果有就用用户配置的，如果没有，才自动配置；如果有些组件可以有多个（**ViewResolver**）将用户配置的和自己默认的组合起来；

2）在 **SpringBoot** 中会有非常多的 **xxxConfigurer** 帮助我们进行扩展配置

3）在 **SpringBoot** 中会有很多的 **xxxCustomizer** 帮助我们进行定制配置



## 6、Restful CRUD

### 1）默认访问首页

```java
//使用 WebMvcConfigurerAdapter 可以来扩展 SpringMVC 的功能
//@EnableWebMvc  不要接管SpringMVC
@Configuration
public class MyMvcConfig extends WebMvcConfigurerAdapter {

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        // super.addViewControllers(registry);
        //浏览器发送 /superbeyone 请求来到 success
        registry.addViewController("/superbeyone").setViewName("success");
    }

    //所有的 WebMvcConfigurerAdapter 组件都会一起起作用
    @Bean //将组件注册在容器
    public WebMvcConfigurerAdapter webMvcConfigurerAdapter(){
        WebMvcConfigurerAdapter adapter = new WebMvcConfigurerAdapter() {
            @Override
            public void addViewControllers(ViewControllerRegistry registry) {
                registry.addViewController("/").setViewName("login");
                registry.addViewController("/index.html").setViewName("login");
            }
        };
        return adapter;
    }
}
```



### 2）国际化

在以前的 SpringMVC 中，国际化需要以下3步骤

1）编写国际化配置文件；

2）使用ResourceBundleMessageSource管理国际化资源文件；

3）在页面使用fmt:message取出国际化内容；

步骤：

**1）编写国际化配置文件，抽取页面需要显示的国际化消息**

![1592523397_1_.png](https://s2.loli.net/2022/02/16/5oFMwsVKy7Cd4qA.png)



**2）spring boot 自动配置好了管理国际化资源文件的组件**

我们只需要在配置文件中指定国际化资源文件的位置 `spring.messages.basename=i18n.login`              

```java
@ConfigurationProperties(prefix = "spring.messages")
public class MessageSourceAutoConfiguration {
    /**
     * Comma-separated list of basenames (essentially a fully-qualified classpath
     * location), each following the ResourceBundle convention with relaxed support for
     * slash based locations. If it doesn't contain a package qualifier (such as
     * "org.mypackage"), it will be resolved from the classpath root.
     */ 
    private String basename = "messages";  
    //我们的配置文件可以直接放在类路径下叫 messages.properties；

    @Bean
    public MessageSource messageSource() {
        ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
        if (StringUtils.hasText(this.basename)) {
            //设置国际化资源文件的基础名（去掉语言国家代码的）
            messageSource.setBasenames(StringUtils.commaDelimitedListToStringArray(
                StringUtils.trimAllWhitespace(this.basename)));
        }
        if (this.encoding != null) {
            messageSource.setDefaultEncoding(this.encoding.name());
        }
        messageSource.setFallbackToSystemLocale(this.fallbackToSystemLocale);
        messageSource.setCacheSeconds(this.cacheSeconds);
        messageSource.setAlwaysUseMessageFormat(this.alwaysUseMessageFormat);
        return messageSource;
    }
```

​         

**3）在页面获取国际化的值**

**通过thymeleaf的 #{message}** 

![clipboard _8_.png](https://s2.loli.net/2022/02/16/LNnuAq9hRSfOHYr.png)

```html
<body class="text-center">
    <form class="form-signin" action="dashboard.html" th:action="@{/user/login}" method="post">
        <img class="mb-4" src="asserts/img/bootstrap-solid.svg" alt="" width="72" height="72">
        <h1 class="h3 mb-3 font-weight-normal" th:text="#{login.tip}">Please sign in</h1>
        <p style="color: red" th:text="${msg}" th:if="${not #strings.isEmpty(msg)}"></p>
        <label class="sr-only" th:text="#{login.username}">Username</label>
        <input type="text" name="username" class="form-control" placeholder="Username" th:placeholder="#{login.username}" required="" autofocus="">
        <label class="sr-only" th:text="#{login.password}">Password</label>
        <input type="password" name="password" class="form-control" placeholder="Password" th:placeholder="#{login.password}"
requined="">
        <div class="checkbox mb-3">
            <label>
                <input type="checkbox" value-"remember-me"> [[#{login.remember}]]
            </label>
        </div>
        <button class-"btn btn-lg btn-primary btn-block" type-"submit" th:tex </button>
        <p class="mt-5 mb-3 text-muted">@ 2022-01</p>
        <a class="btn btn-sm" th:href-"@{/index(l="zh_CN")}" >中文</a>
        <a class="btn btn-sm" th:href="@{/index(l="en_US")}">English</a>
    </form>
</body>
```

**效果：根据浏览器语言设置的信息切换了国际化；**

**4）原理：**

国际化 Locale（区域信息对象）；LocaleResolver（获取区域信息对象）；

```java
@Bean
@ConditionalOnMissingBean
@ConditionalOnProperty(prefix = "spring.mvc", name = "locale")
public LocaleResolver localeResolver() {
    if (this.mvcProperties
        .getLocaleResolver() == WebMvcProperties.LocaleResolver.FIXED) {
        return new FixedLocaleResolver(this.mvcProperties.getLocale());
    }
    AcceptHeaderLocaleResolver localeResolver = new AcceptHeaderLocaleResolver();
    localeResolver.setDefaultLocale(this.mvcProperties.getLocale());
    return localeResolver;
}
默认的就是根据请求头带来的区域信息获取 Locale 进行国际化
```

​             

**4）点击链接切换国际化**

前台：thymeleaf 语法，localhost:8080/index

​                <a class="btn btn-sm" th:href="@{/index(l='zh_CN')}" >中文</a> <a class="btn btn-sm" th:href="@{/index(l='en_US')}">English</a>               

```java
/**
 * 可以在连接上携带区域信息
 */
public class MyLocaleResolver implements LocaleResolver {
    
    @Override
    public Locale resolveLocale(HttpServletRequest request) {
        String l = request.getParameter("l");
        Locale locale = Locale.getDefault();
        if(!StringUtils.isEmpty(l)){
            String[] split = l.split("_");
            locale = new Locale(split[0],split[1]);
        }
        return locale;
    }

    @Override
    public void setLocale(HttpServletRequest request, HttpServletResponse response, Locale locale) {

    }
}

========================================================
    @Bean  //给容器加入组件
    public LocaleResolver localeResolver(){
        return new MyLocaleResolver();
    }
```



**效果：**

​    ![0](https://note.youdao.com/yws/public/resource/49d7a6950c927a696392db0665d4838c/xmlnote/03EF9E9261B2492DAF5BA5FCA658796D/19926)

​    ![0](https://note.youdao.com/yws/public/resource/49d7a6950c927a696392db0665d4838c/xmlnote/C2A54B04889B4A6C990B373B72D64D57/19928)

### 3）登录

开发期间模板引擎页面修改以后，要实时生效

1）禁用模板引擎的缓存

​                \# 禁用缓存  `spring.thymeleaf.cache=false`              

2）页面修改完成以后 `ctrl+f9`；重新编译

登陆错误消息的显示

```html
<p style="color: red" th:text="${msg}" th:if="${not #strings.isEmpty(msg)}"></p>
```



### 4）拦截器实现登录检查

自定义拦截器

```java
/**
 * 登陆检查
 */
public class LoginHandlerInterceptor implements HandlerInterceptor {
    //目标方法执行之前
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        Object user = request.getSession().getAttribute("loginUser");
        if(user == null){
            //未登陆，返回登陆页面
            request.setAttribute("msg","没有权限请先登陆");
            request.getRequestDispatcher("/index.html").forward(request,response);
            return false;
        }else{
            //已登陆，放行请求
            return true;
        }
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {

    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }
}
```

注册拦截器

```java
// 所有的 WebMvcConfigurerAdapter 组件都会一起起作用
// 将组件注册在容器
@Bean 
public WebMvcConfigurerAdapter webMvcConfigurerAdapter(){
    WebMvcConfigurerAdapter adapter = new WebMvcConfigurerAdapter() {
        @Override
        public void addViewControllers(ViewControllerRegistry registry) {
            registry.addViewController("/").setViewName("login");
            registry.addViewController("/index.html").setViewName("login");
            registry.addViewController("/main.html").setViewName("dashboard");
        }

        //注册拦截器
        @Override
        public void addInterceptors(InterceptorRegistry registry) {
            //super.addInterceptors(registry);
            //静态资源；  *.css , *.js
            //SpringBoot已经做好了静态资源映射
            registry.addInterceptor(new LoginHandlerInterceptor()).addPathPatterns("/**")
                .excludePathPatterns("/index.html","/","/user/login");
        }
    };
    return adapter;
}
```



### 5）CRUD-员工列表

实验要求：

1）RestfulCRUD：CRUD满足 Rest 风格；

URI： /资源名称/资源标识   HTTP请求方式区分对资源   CRUD操作

|      |      Restful  CRUD      | Restful   CRUD  |
| :--: | :---------------------: | :-------------: |
| 查询 |         getEmp          |     emp—GET     |
| 添加 |       addEmp?xxx        |    emp—POST     |
| 修改 | updateEmp?id=xxx&xxx=xx |  emp/{id}—PUT   |
| 删除 |     deleteEmp?id=1      | emp/{id}—DELETE |



2）实验的请求架构;

|               实验功能               | 请求URI | 请求方式 |
| :----------------------------------: | :-----: | :------: |
|             查询所有员工             |  emps   |   GET    |
|      查询某个员工(来到修改页面)      |  emp/1  |   GET    |
|             来到添加页面             |   emp   |   GET    |
|               添加员工               |   emp   |   POST   |
| 来到修改页面（查出员工进行信息回显） |  emp/1  |   GET    |
|               修改员工               |   emp   |   PUT    |
|               删除员工               |  emp/1  |  DELETE  |



**thymeleaf公共页面元素抽取**

```html
1、抽取公共片段
<div th:fragment="copy">
&copy; 2011 The Good Thymes Virtual Grocery
</div>

2、引入公共片段
<div th:insert="~{footer :: copy}"></div>
~{templatename::selector}：模板名::选择器
~{templatename::fragmentname}:模板名::片段名

3、默认效果：
insert的公共片段在div标签中
如果使用th:insert等属性进行引入，可以不用写~{}：
行内写法可以加上：[[~{}]];[(~{})]；
```

三种引入公共片段的 th 属性：

**th:insert**：将公共片段整个插入到声明引入的元素中

**th:replace**：将声明引入的元素替换为公共片段

**th:include**：将被引入的片段的内容包含进这个标签中

```html
<footer th:fragment="copy">
&copy; 2011 The Good Thymes Virtual Grocery
</footer>

引入方式
<div th:insert="footer :: copy"></div>
<div th:replace="footer :: copy"></div>
<div th:include="footer :: copy"></div>

效果
<div>
    <footer>
    &copy; 2011 The Good Thymes Virtual Grocery
    </footer>
</div>

<footer>
&copy; 2011 The Good Thymes Virtual Grocery
</footer>

<div>
&copy; 2011 The Good Thymes Virtual Grocery
</div>
```



引入片段的时候传入参数：      

```html
<nav class="col-md-2 d-none d-md-block bg-light sidebar" id="sidebar">
    <div class="sidebar-sticky">
        <ul class="nav flex-column">
            <li class="nav-item">
                <a class="nav-link active"
                   th:class="${activeUri=='main.html'?'nav-link active':'nav-link'}"
                   href="#" th:href="@{/main.html}">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-home">
                        <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                        <polyline points="9 22 9 12 15 12 15 22"></polyline>
                    </svg>
                    Dashboard <span class="sr-only">(current)</span>
                </a>
            </li>

<!--引入侧边栏;传入参数-->
<div th:replace="commons/bar::#sidebar(activeUri='emps')"></div>
```



### 6）CRUD-员工添加

```html
<form>
    <div class="form-group">
        <label>LastName</label>
        <input type="text" class="form-control" placeholder="zhangsan">
    </div>
    <div class="form-group">
        <label>Email</label>
        <input type="email" class="form-control" placeholder="zhangsan@superbeyone.com">
    </div>
    <div class="form-group">
        <label>Gender</label><br/>
        <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="gender"  value="1">
            <label class="form-check-label">男</label>
        </div>
        <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="gender"  value="0">
            <label class="form-check-label">女</label>
        </div>
    </div>
    <div class="form-group">
        <label>department</label>
        <select class="form-control">
            <option>1</option>
            <option>2</option>
            <option>3</option>
            <option>4</option>
            <option>5</option>
        </select>
    </div>
    <div class="form-group">
        <label>Birth</label>
        <input type="text" class="form-control" placeholder="zhangsan">
    </div>
    <button type="submit" class="btn btn-primary">添加</button>
</form>
```

> 提交的数据格式不对：生日：日期；
>
> 2017-12-12；2017/12/12；2017.12.12；
>
> 日期的格式化；SpringMVC 将页面提交的值需要转换为指定的类型;
>
> 2017-12-12—Date； 类型转换，格式化;
>
> 默认日期是按照/的方式；

### 7）CRUD-员工修改

修改添加二合一表单

```html
<!--需要区分是员工修改还是添加；-->
<form th:action="@{/emp}" method="post">
    <!--发送put请求修改员工数据-->
    <!--
1、SpringMVC中配置HiddenHttpMethodFilter;（SpringBoot自动配置好的）
2、页面创建一个post表单
3、创建一个input项，name="_method";值就是我们指定的请求方式
-->
    <input type="hidden" name="_method" value="put" th:if="${emp!=null}"/>
    <input type="hidden" name="id" th:if="${emp!=null}" th:value="${emp.id}">
    <div class="form-group">
        <label>LastName</label>
        <input name="lastName" type="text" class="form-control" placeholder="zhangsan" th:value="${emp!=null}?${emp.lastName}">
    </div>
    <div class="form-group">
        <label>Email</label>
        <input name="email" type="email" class="form-control" placeholder="zhangsan@superbeyone.com" th:value="${emp!=null}?${emp.email}">
    </div>
    <div class="form-group">
        <label>Gender</label><br/>
        <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="gender" value="1" th:checked="${emp!=null}?${emp.gender==1}">
            <label class="form-check-label">男</label>
        </div>
        <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="gender" value="0" th:checked="${emp!=null}?${emp.gender==0}">
            <label class="form-check-label">女</label>
        </div>
    </div>
    <div class="form-group">
        <label>department</label>
        <!--提交的是部门的id-->
        <select class="form-control" name="department.id">
            <option th:selected="${emp!=null}?${dept.id == emp.department.id}" th:value="${dept.id}" th:each="dept:${depts}" th:text="${dept.departmentName}">1</option>
        </select>
    </div>
    <div class="form-group">
        <label>Birth</label>
        <input name="birth" type="text" class="form-control" placeholder="zhangsan" th:value="${emp!=null}?${#dates.format(emp.birth, 'yyyy-MM-dd HH:mm')}">
    </div>
    <button type="submit" class="btn btn-primary" th:text="${emp!=null}?'修改':'添加'">添加</button>
</form>
```



### 8）CRUD-员工删除

```html
<tr th:each="emp:${emps}">
    <td th:text="${emp.id}"></td>
    <td>[[${emp.lastName}]]</td>
    <td th:text="${emp.email}"></td>
    <td th:text="${emp.gender}==0?'女':'男'"></td>
    <td th:text="${emp.department.departmentName}"></td>
    <td th:text="${#dates.format(emp.birth, 'yyyy-MM-dd HH:mm')}"></td>
    <td>
        <a class="btn btn-sm btn-primary" th:href="@{/emp/}+${emp.id}">编辑</a>
        <button th:attr="del_uri=@{/emp/}+${emp.id}" class="btn btn-sm btn-danger deleteBtn">删除</button>
    </td>
</tr>


<script>
    $(".deleteBtn").click(function(){
        //删除当前员工的
        $("#deleteEmpForm").attr("action",$(this).attr("del_uri")).submit();
        return false;
    });
</script>
```



## 7、错误处理机制

### 1）SpringBoot错误的默认处理机制

默认效果：

​	1）浏览器，返回一个默认的错误页面

​    ![180226173408.png](https://s2.loli.net/2022/02/16/6Tt3fEyieJg8sQI.png)

​	2）、如果是其他客户端，默认响应一个json数据

​    ![180226173527.png](https://s2.loli.net/2022/02/16/eChpVgm8IinoJG2.png)

​		

### 2）如何定制错误响应

**1）如何定制错误的页面？**

- 有模板引擎的情况下；error/状态码; 【将错误页面命名为  错误状态码 .html  放在模板引擎文件夹里面的 error 文件夹下】，发生此状态码的错误就会来到对应的页面

- 我们可以使用 4xx 和 5xx 作为错误页面的文件名来匹配这种类型的所有错误，精确优先（ 优先寻找精确的状态码.html ）
- 页面能获取的信息
  - timestamp：时间戳
  - status：状态码
  - error：错误提示
  - exception：异常对象
  - message：异常消息
  - errors：JSR303数据校验的错误都在这里

- 没有模板引擎（模板引擎找不到这个错误页面），静态资源文件夹下找

- 以上都没有错误页面，就是默认来到 SpringBoot 默认的错误提示页面	

​    ![clipboard _9_.png](https://s2.loli.net/2022/02/16/GYviOjnqHM7B4gp.png)

![clipboard _10_.png](https://s2.loli.net/2022/02/16/tl2cZNV7aCRbeG8.png)

**2）如何定制错误的 json 数据**

- 自定义异常处理&返回定制 json 数据

```java
@ControllerAdvice 
public class MyExceptionHandler {   
    //浏览器和客户端返回的都是json  
    @ResponseBody  
    @ExceptionHandler(UserNotExistException.class)  
    public Map<String,Object> handleException(Exception e){  
        Map<String,Object> map = new HashMap<>();  
        map.put("code", "user.notexists");   
        map.put("message",e.getMessage());    
        return map;  
    }
} //没有自适应效果...           
```

- 转发到 /error 进行自适应响应效果处理

```java
@ControllerAdvice 
public class MyExceptionHandler {   
    @ExceptionHandler(UserNotExistException.class)
    public String handleException(HttpServletRequest request,Exception e){   
        Map<String,Object> map = new HashMap<>();       
        //传入我们自己的错误状态码     
        request.setAttribute("javax.servlet.error.status_code", 400);   
        map.put("code", "user.notexists");    
        map.put("message",e.getMessage());    
        request.setAttribute("etx", map);      
        return "forword:/error";   
    }
}            
```

- 将我们的定制数据携带出去（携带到页面，或者响应的 json 字符串）
- 出现错误以后，会来到 /error 请求，会被 `BasicErrorController` 处理，响应出去可以获取的数据是由 `getErrorAttributes` 得到的（是`AbstractErrorController（ErrorController）`规定的方法）
  - 完全来编写一个 `ErrorController` 的实现类【或者是编写 `AbstractErrorController` 的子类】，放在容器中
  - 页面上能用的数据，或者是 json 返回能用的数据都是通过 `errorAttributes.getErrorAttributes` 得到
- 容器中 `DefaultErrorAttributes.getErrorAttributes()；`默认进行数据处理的
- 自定义 `ErrorAttributes`

```java
//给容器中加入我们自己定义的 ErrorAttributes 
@Component
public class MyErrorAttributes extends DefaultErrorAttributes {    
    @Override    
    public Map<String, Object> getErrorAttributes(WebRequest webRequest, boolean includeStackTrace) {     
        Map<String, Object> errorAttributes = super.getErrorAttributes(webRequest, includeStackTrace);
        errorAttributes.put("personal", "houchen");    
        Map<String,Object> etx = (Map<String,Object>)webRequest.getAttribute("etx", 0);    
        errorAttributes.put("etx", etx);     
        return errorAttributes;  
    }
}      
```

![clipboard _11_.png](https://s2.loli.net/2022/02/16/dmDqhPHeBxiGvT9.png)



## 8、配置嵌入式 Servlet 容器

### 1）如何定制和修改Servlet容器的相关配置

- 修改和 server 有关的配置（ServerProperties【也是 EmbeddedServletContainerCustomizer】）

```properties
server.port=8081 
server.context-path=/crud 
server.tomcat.uri-encoding=UTF-8 //通用的Servlet容器设置
server.xxx=xxx    //Tomcat的设置 
server.tomcat.xxx=xxx         
```

​     

- 编写一个 **EmbeddedServletContainerCustomizer**：嵌入式的 Servlet 容器的定制器，来修改Servlet容器的配置

```java
@Bean  //一定要将这个定制器加入到容器中 
public EmbeddedServletContainerCustomizer embeddedServletContainerCustomizer(){
    return new EmbeddedServletContainerCustomizer() {
        //定制嵌入式的Servlet容器相关的规则
        @Override
        public void customize(ConfigurableEmbeddedServletContainer container) {
            container.setPort(8083);
        }
    };
}
```

【注意】 springboot 2.0.1以上

```java
// server 相关的配置类 
public class MyServerConfig {   
    //编写一个 EmbeddedServletContainerCustomizer： 
    //嵌入式的 Servlet 容器的定制器，来修改Servlet容器的配置   
    @Bean  //一定要将这个定制器加入到容器中   
    public WebServerFactoryCustomizer<ConfigurableWebServerFactory> webServerFactoryCustomizer(){    
        return new WebServerFactoryCustomizer<ConfigurableWebServerFactory>() {    
            @Override         
            public void customize(ConfigurableWebServerFactory factory) {       
                factory.setPort(8081);        
            }   
        };  
    } 
}              
```



### 2）注册 Servlet 三大组件【Servlet、Filter、Listener】

由于 SpringBoot 默认是以 jar 包的方式启动嵌入式的 servlet 容器来启动 SpringBoot 的 web 应用，没有 **`web.xml`** 文件。

```java
//注册三大组件 
//servlet 
@Bean 
public ServletRegistrationBean myServlet(){   
    ServletRegistrationBean registrationBean = new ServletRegistrationBean(new MyServlet(),"/myServlet");  
    return registrationBean;
} 

//filter
@Bean
public FilterRegistrationBean myFilter(){  
    FilterRegistrationBean registrationBean = new FilterRegistrationBean(); 
    registrationBean.setFilter(new MyFilter());  
    registrationBean.setUrlPatterns(Arrays.asList("/hello","/myServlet"));   
    return registrationBean;
} 

//Listener
@Bean
public ServletListenerRegistrationBean myListener(){  
    ServletListenerRegistrationBean<MyListener> registrationBean = new ServletListenerRegistrationBean<>(new MyListener()); 
    return registrationBean;
}              
```

SpringBoot 帮我们自动 SpringMVC 的时候，自动的注册S pringMVC 的前端控制器：**DIspatcherServlet**

**DispatcherServletAutoConfiguration** 中：

```java
@Bean(name = DEFAULT_DISPATCHER_SERVLET_REGISTRATION_BEAN_NAME) 
@ConditionalOnBean(value = DispatcherServlet.class, name = DEFAULT_DISPATCHER_SERVLET_BEAN_NAME)
public ServletRegistrationBean dispatcherServletRegistration(DispatcherServlet dispatcherServlet){  
    ServletRegistrationBean registration = new 
        ServletRegistrationBean(dispatcherServlet,this.serverProperties.getServletMapping());
    //默认拦截： /  所有请求；包静态资源，但是不拦截 jsp 请求；   /* 会拦截所有请求包括，jsp  
    //可以通过 server.servletPath 来修改 SpringMVC 前端控制器默认拦截的请求路径  
    registration.setName(DEFAULT_DISPATCHER_SERVLET_BEAN_NAME);  
    registration.setLoadOnStartup(this.webMvcProperties.getServlet().getLoadOnStartup());  
    if (this.multipartConfig != null) {   
        registration.setMultipartConfig(this.multipartConfig);  
    } 
    return registration; 
}              
```



### 3）替换为其他嵌入式Servlet容器

**jetty**：是一个提供 HHTP 服务器、HTTP客户端和 javax.servlet 容器的开源项目。

```xml
<!-- 引入web模块 -->
<dependency>
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-web</artifactId>   
    <exclusions>   
        <exclusion>        
            <artifactId>spring-boot-starter-tomcat</artifactId>     
            <groupId>org.springframework.boot</groupId>   
        </exclusion>  
    </exclusions> 
</dependency> 

<!--引入其他的Servlet容器--> 
<dependency> 
    <artifactId>spring-boot-starter-jetty</artifactId>  
    <groupId>org.springframework.boot</groupId>
</dependency> 
```



### 4）嵌入式Servlet容器自动配置原理

**步骤：**

- SpringBoot 根据导入的依赖情况，给容器中添加相应的 **`EmbeddedServletContainerFactory【TomcatEmbeddedServletContainerFactory】`**

- 容器中某个组件要创建对象就会惊动后置处理器，**`EmbeddedServletContainerCustomizerBeanPostProcessor`**，只要是嵌入式的 Servlet 容器工厂，后置处理器就工作

- 后置处理器，从容器中获取所有的 **`EmbeddedServletContainerCustomizer`**，调用定制器的定制方法



### 5）嵌入式Servlet容器启动原理

1）SpringBoot 应用启动运行 run 方法

2）**refreshContext(context)**：SpringBoot 刷新 IOC 容器【创建 IOC 容器对象，并初始化容器，创建容器中的每一个组件】；如果是 web 应用创建`AnnotationConfigEmbeddedWebApplicationContext`，否则：`AnnotationConfigApplicationContext`

3）**refresh(context)**：**刷新刚才创建好的 IOC 容器**

4）**onRefresh()**： web的 ioc 容器重写了onRefresh方法

5）Web IOC容器会创建嵌入式的Servlet容器  ===》**createEmbeddedServletContainer**()

6）获取嵌入式的Servlet容器工厂：`EmbeddedServletContainerFactory containerFactory = getEmbeddedServletContainerFactory();`

​	从 ioc 容器中获取 `EmbeddedServletContainerFactory`  组件；`TomcatEmbeddedServletContainerFactory` 创建对象，后置处理器一看是这个对象，就获	取所有的定制器来先定制Servlet容器的相关配置

7）**使用容器工厂获取嵌入式的Servlet容器：**

​	`this.embeddedServletContainer = containerFactory.getEmbeddedServletContainer(getSelfInitializer());`

8）嵌入式的Servlet容器创建对象并启动Servlet容器

​	先启动嵌入式的Servlet容器，再将 ioc 容器中剩下没有创建出的对象获取出来；

​	IOC容器启动创建嵌入式的Servlet容器



## 9、使用外置的Servlet容器

1）必须创建一个 war 项目（利用 idea 创建好目录结构）

2）将嵌入式的 Tomcat 指定为 **provided**

```xml
<dependency>   
    <groupId>org.springframework.boot</groupId> 
    <artifactId>spring-boot-starter-tomcat</artifactId> 
    <scope>provided</scope> 
</dependency>  
```

3）必须编写一个 **SpringBootServletInitializer** 的子类，并调用 configure 方法

```java
public class ServletInitializer extends   {    
    @Override  
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {   
        //传入SpringBoot应用的主程序  
        return application.sources(SpringBoot04WebJspApplication.class);
    }
}              
```

4）启动服务器就可以使用





# 五、docker的使用 

文档资料 ：https://docs.docker.com/get-started/

## 1、简介

![clipboard _12_.png](https://s2.loli.net/2022/02/16/Dxq6G7UEW8ynhOs.png)

## 2、docker核心概念

docker 主机(Host)：安装了 Docker 程序的机器（ Docker 直接安装在操作系统之上）

docker 客户端(Client)：连接docker主机进行操作

docker 仓库(Registry)：用来保存各种打包好的软件镜像

docker 镜像(Images)：软件打包好的镜像；放在docker仓库中

docker 容器(Container)：镜像启动后的实例称为一个容器；容器是独立运行的一个或一组应用

**使用 Docker 的步骤：**

- 安装docker

- 去docker仓库中拉取对应的镜像

- 使用docker运行这个镜像，这个镜像就会生成一个Docker容器

- 对容器的启动停止就是对软件的启动停止

## 3、Docker环境准备

安装 docker：one：https://www.runoob.com/docker/centos-docker-install.html

two：https://yeasy.gitbook.io/docker_practice/install/windows

 

## 4、docker中的常用操作

**1）镜像操作**

- 搜索镜像

  docker serach  xxx  

- 拉取镜像

  docker pull 镜像名

- 查看本地的所有镜像

  docker images

- 删除本地镜像

  docker rmi 镜像ID

**2）容器操作**

- 启动容器

  docker run --name xxx(自定义名称) -d 镜像名称(ID)

- 查看运行中的所有容器

  docker ps

- 停止运行中的容器

  docker stop 容器的名称（Id）

- 查看所有容器

  docker ps -a

- 删除容器

  docker rm 容器Id

- 启动容器

  docker start 容器Id

**3）端口映射**

**-p  8088:8080       主机端口映射到容器内部端口**

 **docker run -d -p 8088:8080 --name mytomcat tomcat**

![clipboard _13_.png](https://s2.loli.net/2022/02/16/FOdgLzSY6cNjf1B.png)



遇到的问题：[**docker添加tomcat容器成功无法访问首页**](https://www.cnblogs.com/houchen/p/13059056.html)

https://www.cnblogs.com/houchen/p/13059056.html

![clipboard _14_.png](https://s2.loli.net/2022/02/16/sfRgUMNeJZvqy1G.png)



## 5、docker安装mysql

`docker run --name mysql_5.6 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6`    

![clipboard _15_.png](https://s2.loli.net/2022/02/16/pe9d2fP8vD5oXh6.png)





# 六、SpringBoot_数据访问

## 1、JDBC

### 1）依赖 

> 可以选择自己导入，也可以使用 Spring Initializr 初始化一个SpringBoot项目，就可直接生成 pom.xml，所需要的依赖也会自动导入完成。

```xml
<parent>    
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-parent</artifactId>    
    <version>2.0.1.RELEASE</version>    
    <relativePath/> 
    <!-- lookup parent from repository --> 
</parent>  

<groupId>com.atguigu</groupId> 
<artifactId>spring-boot-06-data-jdbc</artifactId> 
<version>1.0-SNAPSHOT</version>  

<dependencies>   
    <dependency>      
        <groupId>org.springframework.boot</groupId>   
        <artifactId>spring-boot-starter-jdbc</artifactId> 
    </dependency>   
    <dependency>     
        <groupId>mysql</groupId>      
        <artifactId>mysql-connector-java</artifactId>     
        <scope>runtime</scope>     
    </dependency>    
    <!--引入druid数据源-->  
    <!-- https://mvnrepository.com/artifact/com.alibaba/druid -->  
    <dependency>    
        <groupId>com.alibaba</groupId>     
        <artifactId>druid</artifactId>     
        <version>1.1.6</version>  
    </dependency>   
    <dependency>     
        <groupId>org.springframework.boot</groupId>     
        <artifactId>spring-boot-starter-web</artifactId>  
    </dependency>    
    <dependency>      
        <groupId>org.springframework.boot</groupId>    
        <artifactId>spring-boot-starter-test</artifactId>  
        <scope>test</scope>  
    </dependency> </dependencies>  

<build>   
    <plugins>       
        <plugin>          
            <groupId>org.springframework.boot</groupId>      
            <artifactId>spring-boot-maven-plugin</artifactId>     
        </plugin>  
    </plugins>
</build>       
```

### 2）配置文件

```yaml
spring:
    datasource:   
    username: root   
    password: 123456 
    url: jdbc:mysql://127.0.0.1:3306/springboot_jdbc  
    driver-class-name: com.mysql.jdbc.Driver   
```

### 3）测试

```java
@RunWith(SpringRunner.class) 
@SpringBootTest 
public class SpringBootDataJdbcApplicationText {    
    @Autowired   
    private DataSource dataSource;    
    @Test 
    public void test() throws SQLException {   
        System.out.println(dataSource.getClass());      
        Connection connection = dataSource.getConnection();     
        System.out.println(connection);     
        connection.close();  
    } 
}        
```

可以看到 `spring-boot 2.0.1.RELEASE` 默认采用的连接池为：

​    ![0](https://note.youdao.com/yws/public/resource/49d7a6950c927a696392db0665d4838c/xmlnote/906E76A44D584380A51C58D1B08F08A8/25529)

> 在数据源创建的同时执行建表语句：schema-.sql、data-.sql 
>
> 默认规则：schema.sql，schema-all.sql
>
> 也可以配置    schema:      - classpath:department.sql      指定位置              



## 2、整合Druid数据源

```java
@Configuration public class DruidConfig {   
    
    @ConfigurationProperties(prefix = "spring.datasource")   
    @Bean  
    public DataSource druid(){    
        return  new DruidDataSource();  
    }    
    
    //配置Druid的监控    
    //1、配置一个管理后台的Servlet   
    @Bean    
    public ServletRegistrationBean statViewServlet(){ 
        ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");   
        Map<String,String> initParams = new HashMap<>();      
        initParams.put("loginUsername","admin");      
        initParams.put("loginPassword","123456");      
        initParams.put("allow","");//默认就是允许所有访问   
        initParams.put("deny","192.168.15.21"); //拒绝谁来访问     
        bean.setInitParameters(initParams);     
        return bean;    
    }   
    
    //2、配置一个web监控的filter   
    @Bean   
    public FilterRegistrationBean webStatFilter(){   
        FilterRegistrationBean bean = new FilterRegistrationBean();    
        bean.setFilter(new WebStatFilter());     
        Map<String,String> initParams = new HashMap<>();    
        initParams.put("exclusions","*.js,*.css,/druid/*");    
        bean.setInitParameters(initParams);       
        bean.setUrlPatterns(Arrays.asList("/*"));      
        return  bean;   
    }
}              
```

<img src="https://s2.loli.net/2022/02/16/Rb6honDTIkNJKZA.png" alt="clipboard _16_.png" style="zoom:80%;" />



## 3、整合MyBatis

### 1）注解版

**自定义 MyBatis 的配置规则：给容器中添加一个 ConfigurationCustomizer。**

```java
@org.springframework.context.annotation.Configuration 
    public class MyBatisConfig {   
        @Bean   
        public ConfigurationCustomizer configurationCustomizer(){  
            return new ConfigurationCustomizer(){      
                @Override      
                public void customize(Configuration configuration) {   
                    configuration.setMapUnderscoreToCamelCase(true); 
                }     
            };  
        } 
    }   
```

### 2）xml配置版

```yaml
mybatis:  # 指定全局配置文件位置 
	config-location: classpath:mybatis/mybatis-config.xml  # 指定 sql 映射文件位置  
	mapper-locations: classpath:mybatis/mapper/*.xml              
```



## 4、整合SpringData JPA

### 1）SpringData简介

![clipboard _17_.png](https://s2.loli.net/2022/02/16/LvkOBY1F82jKsyI.png)

### 2）整合 SpringData jpa





# 七、SpringBoot_启动配置原理

参考尚硅谷 SpringBoot 源码分析的原理解析。

# 八、SpringBoot_自定义starters

starter :

1、这个场景需要用到的依赖是什么？

2、如何编写自动配置

