# SPRING5.x

## 简介

```tex
Spring 中文含义 春天
发展历史：
	2002年由悉尼大学音乐系博士Rod Johnson 退出了Spring框架的雏形 Interface21框架
	2004年3月正式发布了Spring1.0版本
理念：
	使现有技术更加容易使用，Spring提供了很多框架的整合技术
        Core technologies: dependency injection, events, resources, i18n, validation, 		  data binding, type conversion, SpEL, AOP.
        Testing: mock objects, TestContext framework, Spring MVC Test, WebTestClient.
        Data Access: transactions, DAO support, JDBC, ORM, Marshalling XML.
        Spring MVC and Spring WebFlux web frameworks.
        Integration: remoting, JMS, JCA, JMX, email, tasks, scheduling, cache.
        Languages: Kotlin, Groovy, dynamic languages.
        
Spring官方文档
	 http://repo.spring.io/release/org/springframework/spring
	 在线文档
	 https://docs.spring.io/spring-framework/docs/5.2.24.RELEASE/spring-framework-reference/core.html#spring-core
	 
Spring源码
	http://github.com/spring-projects/spring-framework
	
Spring是免费开源的框架，是一个轻量级 非入侵式的框架

Spring特点
	IOC（控制反转）、AOP（面向切面编程）
	支持事务的处理，对各种框架整合的支持
```

![image-20230416230308551](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230416230308551.png)

### Spring需要的依赖

```
<!-- https://mvnrepository.com/artifact/org.springframework/spring-core -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.3.23</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-web -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
    <version>5.3.23</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.23</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.23</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.23</version>
</dependency>

```



### Spring的7大组件

```
其中组成Spring框架的每个模块都可以单独存在，或者可以与其他一个或多个模块联合实现

1. 核心容器SpringCode： 核心容器提供Spring框架的基本功能。—-它主要的组件就是BeanFactory,是工厂模式的实现。同时BeanFactory适用控制反转（IOC）思想将应用程序的配置和依赖性规范与实际的应用程序分开。
2. Spring Context： Spring上下文是一个配置文件，主要向框架提供上下文信息。
3. SpringAop： 通过配置管理特性，SpringAOP模块直接将面向切面地编程功能集成到了Spring框架中，所以，它可以很容易地使Spring框架管理的任何对象支持AOP。SpringAOP模块也是基于Spring的应用程序中的对象提供了事务管理服务。—–比较强大的功能
4. SpringDAO： 它主要和dao层相关联,可以用该结构来管理异常处理和不同数据库供应商抛出的错误信息。其中异常层次结构简化了错误处理，并且极大地降低了需要编写地异常代码数据（例如打开和关闭连接）。
5. Spring ORM ： Spring框架中插入了若干个ORM框架，从而提供了ORM的对象关系工具，其中包括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。
6. SpringWEB模块： Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。
7. SpringMVC：MVC 框架是一个全功能的构建 Web 应用程序的 MVC 实现。通过策略接口，MVC 框架变成为高度可配置的，MVC 容纳了大量视图技术，其中包括 JSP、FreeMarker、Velocity、Tiles（jsp布局）、iText（报表处理） 和 poi
```



![image-20230416231015567](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230416231015567.png)

### 扩展

```
现代化的Java开发就是基于Spring的开发
SpringBoot
	是一个快速开发的脚手架 基于SpringBoot可以快速开发单体应用 也可以开发微服务应用
	由于Spring的配置会随着各种框架的整合 导致配置非常繁琐 因此出现了SpringBoot
	
SpringCloud
	是基于SpringBoot实现的 用来管理SpringBoot的应用流程
	
现在大部分公司都在使用SpringBoot快速开发应用 而学习SpringBoot之前必须完全掌握Spring及SpringMVC的应用

```

## IOC

```
```



![image-20230417002917695](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417002917695.png)

![image-20230417003157906](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417003157906.png)

![image-20230417003415163](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417003415163.png)

控制反转理解图

![image-20230417003106796](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417003106796.png)

![image-20230417003312202](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417003312202.png)

新建maven项目 并添加依赖

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.etjava</groupId>
    <artifactId>spring5_1</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
    	<!-- webmvc依赖会将所依赖的包一并下载 因此导入这一个就可以完成大部分功能 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.23</version>
        </dependency>

    </dependencies>

</project>
```

### 创建ioc模块

选中项目 右键 -> New -> Module

![image-20230416235044691](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230416235044691.png)

### UserDao

```java
package com.etjava.dao;

public interface UserDao {
    void findUser();
}

```

#### UserDaoImpl

```java
package com.etjava.dao.impl;

import com.etjava.dao.UserDao;

public class UserDaoImpl implements UserDao {
    @Override
    public void findUser() {
        System.out.println("默认获取用户数据的方法");
    }
}

```

```java
package com.etjava.dao.impl;

import com.etjava.dao.UserDao;

public class UserOrderDaoImpl implements UserDao {
    @Override
    public void findUser() {
        System.out.println("获取用户订单数据的方法");
    }
}

```



#### UserService

```java
package com.etjava.service;

public interface UserService {
    void findUser();
}

```

#### UserServiceImpl

```java
package com.etjava.service;

import com.etjava.dao.UserDao;
import com.etjava.dao.impl.UserDaoImpl;

public class UserServiceImpl implements UserService{

    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void findUser() {
        System.out.println("处理获取用户数据的方法");
        userDao.findUser();
    }
}

```

#### Test

```java
package com.etjava.test;

import com.etjava.dao.impl.UserDaoImpl;
import com.etjava.dao.impl.UserOrderDaoImpl;
import com.etjava.service.UserService;
import com.etjava.service.UserServiceImpl;

public class Test {
    public static void main(String[] args) {
        UserServiceImpl userService = new UserServiceImpl();
        userService.setUserDao(new UserOrderDaoImpl());
        userService.findUser();
    }
}

```

上述方式是传统模式 即 我们在调用的时候自己创建对象，但这种方式有一个很大的弊端 就是后期的维护成本会相对较高，例如 客户修改了需求 我们就需要整体通读一遍我们写的代码 然后找出所有与之相关的代码进行修改 

应对此种方式 我们在Service实现层借助set方法注入 这样就可以减少大量的修改工作

这种设计就是IOC的思维模式

在这种设计之前 对象的创建在程序员手上，使用了set方法注入后 程序员不在具有主动性，而变成了被动接收对象

这种思想从本质上解决了问题 我们程序员不用在管理对象的创建了 有效的降低了系统的耦合性,这种方式可以让我们将精力放在业务是实现上 ==这是IOC的原型==

除了这种set注入方式 还可以使用构造方法传参的注入方式

```java
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
```

 ![image-20230417002859270](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417002859270.png)







