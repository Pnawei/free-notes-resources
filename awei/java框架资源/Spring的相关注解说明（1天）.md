---
title: SpringBoot常用注解
date: 2022-02-11 
tags:
    - 注解
    -  SpringBoot
---

> 申明，本教程使用Intellij IDEA作为java开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

## springboot常用注解

### 1、@SpringBootApplication

包含 @Configuration、@EnableAutoConfiguration、@ComponentScan

通常用在主类上。



### 2、@Repository

用于标注数据访问组件，即DAO组件。



### 3、@Service

用于标注业务层组件。



### 4、@RestController

用于标注控制层组件(如struts中的action)，包含@Controller和@ResponseBody



### 5、@ResponseBody

表示该方法的返回结果直接写入HTTP response body中

一般在异步获取数据时使用，在使用@RequestMapping后，返回值通常解析为跳转路径，加上@responsebody后返回结果不会被解析

为跳转路径，而是直接写入HTTP response body中。比如异步获取json数据，加上@responsebody后，会直接返回json数据。



### 6、@Component

泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注。



### 7、@ComponentScan

组件扫描。相当于<`context:component-scan`>，如果扫描到有@Component @Controller @Service等这些注解的类，则把

这些类注册为bean。



### 8、@Configuration

指出该类是 Bean 配置的信息源，相当于XML中的`<beans></beans>`，一般加在主类上。



### 9、@Bean

相当于XML中的`<bean></bean>`,放在方法的上面，而不是类，意思是产生一个bean,并交给spring管理。



### 10、@EnableAutoConfiguration

让 Spring Boot 根据应用所声明的依赖来对 Spring 框架进行自动配置，一般加在主类上。



### 11、@AutoWired

byType方式。把配置好的Bean拿来用，完成属性、方法的组装，它可以对类成员变量、方法及构造函数进行标注，完成自动装配的工作。

当加上（required=false）时，就算找不到bean也不报错。



### 12、@Qualifier

当有多个同一类型的Bean时，可以用@Qualifier("name")来指定。与@Autowired配合使用



### 13、@Resource(name="name",type="type")

没有括号内内容的话，默认byName。与@Autowired干类似的事。



### 14、@RequestMapping

RequestMapping是一个用来处理请求地址映射的注解，可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。

该注解有六个属性：

params:指定request中必须包含某些参数值是，才让该方法处理。

headers:指定request中必须包含某些指定的header值，才能让该方法处理请求。

value:指定请求的实际地址，指定的地址可以是URI Template 模式

method:指定请求的method类型， GET、POST、PUT、DELETE等

consumes:指定处理请求的提交内容类型（Content-Type），如application/json,text/html;

produces:指定返回的内容类型，仅当request请求头中的(Accept)类型中包含该指定类型才返回



### 15、@RequestParam

用在方法的参数前面。

```java
@RequestParam 
String a =request.getParameter("a")。
```



### 16、@PathVariable

路径变量。参数与大括号里的名字一样要相同。

```java
RequestMapping("user/get/mac/{macAddress}")
public String getByMacAddress(@PathVariable String macAddress){
//do something
}
```



### 17、@Profiles

Spring Profiles提供了一种隔离应用程序配置的方式，并让这些配置只能在特定的环境下生效。

任何@Component或@Configuration都能被@Profile标记，从而限制加载它的时机。

```java
@Configuration
@Profile("prod")
public class ProductionConfiguration { 
	// ...
}
```



### 18、@ConfigurationProperties

Spring Boot将尝试校验外部的配置，默认使用JSR-303（如果在classpath路径中）。

你可以轻松的为你的@ConfigurationProperties类添加JSR-303 javax.validation约束注解：

```java
@Component
@ConfigurationProperties(prefix="connection")
public class ConnectionSettings {
@NotNullprivate InetAddress remoteAddress;
	// ... getters and setters
}
```



### 19、@ControllerAdvice

全局异常处理

包含 @Component。可以被扫描到。

统一处理异常

### 20、@ExceptionHandler（Exception.class）

用在方法上面表示遇到这个异常就执行以下方法









