# Spring

### 1.1  JavaEE分层

- 表现层（页面数据显示、页面跳转调度），例如jsp/servlet 

  ​	Spring:struts1、struts2、Spring MVC

- 业务层（业务处理和功能逻辑、事务控制），例如service

  ​	Spring:Ioc、AOP、事务控制

- 持久层（数据存取和封装、和数据库打交道），例如dao,mapper

  ​	Spring:JdbcTemplate、mybatis、hibernate、springDataJpa框架（对象关系映射）整合



### 1.2  Spring体系结构

### 1.3 Spring优点

1. **方便解耦，简化开发**

   ​	Spring就是一个大工厂，它可以将所有对象创建和依赖关系维护，交给Spring管理

2. AOP**编程的支持**

   ​	Spring提供面向切面编程，可以方便的实现对程序进行权限拦截、运行监控等功能

3. **声明式事务的支持**

   ​	只需要通过配置就可以完成对事务的管理，而无需手动编程

4. **方便程序的测试**

   ​	Spring对Junit4支持，可以通过注解方便的测试Spring程序

5. **方便集成各种优秀框架**

   ​	Spring不排斥各种优秀的开源框架，其内部提供了对各种优秀框架（如：Struts、Hibernate、MyBatis、Quartz等）的直接支持

6. **降低JavaEE API的使用难度**

   ​	Spring 对JavaEE开发中非常难用的一些API（JDBC、JavaMail、远程调用等），都提供了封装，使这些API应用难度大大降低

### 1.4 Spring核心

- ##### IoC（Inverse of Control 控制反转）： 将对象创建权利交给Spring工厂进行管理，解决类与类耦合问题。

- ##### AOP（Aspect Oriented Programming 面向切面编程），基于动态代理的功能增强方式

- ##### 核心包：Beans、Core、Context、SpEL

#### 1.4.1 IoC(控制反转)

1. 底层原理：工厂（设计模式）+反射（机制） + 配置文件（xml）
2. 有了IoC，再用DI动态注入依赖

##### 1.4.1.1 IoC容器装配Bean(XML)

- 四种方式：

  ​	第一种：最常用

  ​	第二、第三种：一些框架初始化的时候用的多。

  ​	第四种:spring底层实现的比较多

##### 1.4.1.2 Bean作用域

- singleton(默认)	单例
- prototype		多例
- request		
- session
- globalSession

##### 1.4.1.3 Bean生命周期

##### 1.4.1.4Bean依赖注入

1. 构造器参数注入
2. setter方法属性注入

#### 1.4.2 AOP

##### 1.4.2.1 场景

- 场景一： 记录日志 
- 场景二： 监控方法运行时间 （监控性能）
- 场景三： 权限控制 
- 场景四： 缓存优化 （第一次调用查询数据库，将查询结果放入内存对象， 第二次调用， 直接从内存对象返回，不需要查询数据库 ）
- 场景五： 事务管理 （调用方法前开启事务， 调用方法后提交或者回滚、关闭事务 ）

##### 1.4.2.2 两种实现方式

- SpringAOP
- AspectJ





​	









​	



