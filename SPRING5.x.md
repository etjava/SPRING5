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
IOC Inversion Of Control  => 控制反转
    是一种设计思想  DI（Dependendy Injection） 依赖注入 是实现IOC的一种方式
    在不使用IOC这种设计理念时 我们使用的是面向对象编程 对象的创建与对象间的依赖关系完全掌握在程序员手中
    使用IOC的设计理念后将对象的创建移交给第三方 我们只需要关注调用及将精力放在核心业务上即可
	所谓的控制反转就是获得所需对象的方式反转了
IOC 是Spring框架的核心内容 使用多种方式完美的实现了IOC
	例如使用XML配置，使用注解方式配置，Configuration配置等
	Spring在初始化时先读取配置文件 然后根据配置文件中的配置创建与组织对象存入到容器中
	我们使用时在从IOC容器中取出需要的对象
	IOC是一种通过扫描(XML或注解)并通过第三方去生产或获取特定对象的方式
	在Spring中 实现控制反转的是IOC Container(IOC 容器)

```

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

## HelloWorld

```
体验IOC的强大之处
	不在创建对象即可调用到对象
采用多模块项目方式  这种方式的好处是不需要在重复导入依赖
```



### 新建模块

选中项目右键 -> New -> Project

![image-20230417190205296](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417190205296.png)

![image-20230417190245842](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417190245842.png)

### 新建实体类User

在src/main/java/com/etjava/model

```java
public class User {
    private String userName;

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    @Override
    public String toString() {
        return "User{" +
                "userName='" + userName + '\'' +
                '}';
    }
}

```

### 添加Spring的核心配置文件

该配置文件内容参考官网 

https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/core.html#spring-core

![image-20230417191459033](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417191459033.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--装配Bean  使用Spring方式创建对象
        我们在创建对象时
            User user = new User();
        使用Spring管理bean
            bean标签相当于new 对象
            id属性相当于对象的名字
            class指定需要创建的对象的全路径
       property 相当于给对象中的属性设置值
    -->
    <bean id="user" class="com.etjava.model.User">
        <!--添加属性的配置-->
        <property name="userName" value="Spring"/>
    </bean>

</beans>
```

### 创建测试类



```java
package com.etjava.test;

import com.etjava.model.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class HelloWorld {
    public static void main(String[] args) {
        // 创建ApplicationContext对象 用来获取Spring的上下文对象
        ApplicationContext context =
                new ClassPathXmlApplicationContext("applicationContext.xml");
        // 在Spring的上下文对象中获取指定的bean
        User user = (User)context.getBean("user");
        System.out.println(user);
    }
}

```

### 小结

```
User对象是由谁来创建的？
	Spring帮我们创建的
User对象的属性值是怎么设置的？
	对象的属性值是由Spring容器设置的
这个过程就叫做控制反转
	控制：谁来控制对象的创建，传统模式 对象是由程序员本身控制创建的，使用Spring后 对象是由Spring来创建
	反转：程序本身不创建对象，而是被动的接收对象
	依赖注入：就是利用set方法进行注入的
	IOC是一种编程思想，有主动的编程变成被动的接收
这样做的优势：
	使用Spring管理和创建Bean 我们就不需要在手动去创建了，只需要在xml配置文件中进行修改即可
总结：
	对象是由Spring来创建，管理和装配
```

查看ClassPathXmlApplicationContext继承树

通过继承树我们可以看到 为什么可以直接使用context上下文对象就能获取到创建好的Bean

因为Spring框架继承了很多相关的类 帮我们处理了创建对象的流程

![image-20230417193309279](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417193309279.png)

### 进一步理解

#### 创建UserDao

```java
package com.etjava.dao;

public interface UserDao {
    void defaultMethod();
}

```

#### 创建UserDao实现类

```java
package com.etjava.dao.impl;

import com.etjava.dao.UserDao;

public class UserDaoImpl implements UserDao {
    @Override
    public void defaultMethod() {
        System.out.println("dao层处理用户数据的默认方法");
    }
}

```

#### 创建UserOrder实现类

实现UserDao接口 目的是为了演示通过spring配置文件进行装配bean

```java
package com.etjava.dao.impl;

import com.etjava.dao.UserDao;

public class UserOrderImpl implements UserDao {
    @Override
    public void defaultMethod() {
        System.out.println("dao层处理用户订单数据的默认方法");
    }
}

```

#### 创建UserService接口

```java
package com.etjava.service;

public interface UserService {
    void test();
}

```

#### 创建UserService实现类

```java
package com.etjava.service;

import com.etjava.dao.UserDao;

public class UserServiceImpl implements UserService{

    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    @Override
    public void test() {
        userDao.defaultMethod();
    }
}

```

#### Spring配置文件中注入UserOrderImpl和UserServiceImpl

并配置UserServiceImpl中的userDao属性

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--装配Bean  使用Spring方式创建对象
        我们在创建对象时
            User user = new User();
        使用Spring管理bean
            bean标签相当于new 对象
            id属性相当于对象的名字
            class指定需要创建的对象的全路径
       property 相当于给对象中的属性设置值
    -->
    <bean id="user" class="com.etjava.model.User">
        <!--添加属性的配置-->
        <property name="userName" value="Spring"/>
    </bean>


    <bean id="userOrderImpl" class="com.etjava.dao.impl.UserOrderImpl"/>

    <bean id="userServiceImpl" class="com.etjava.service.UserServiceImpl">
        <!-- ref 引用Spring中创建好的Bean
            name 表示service实现类中的属性 userDao
        -->
        <property name="userDao" ref="userOrderImpl"/>
    </bean>
</beans>
```

#### 测试

```java
package com.etjava.test;

import com.etjava.service.UserService;
import com.etjava.service.UserServiceImpl;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test2 {
    public static void main(String[] args) {
        // 创建Spring上下文对象
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        // 获取bean  注意 这里获取的bean必须是applicationContext中配置好的
        UserService userServiceImpl = (UserServiceImpl) context.getBean("userServiceImpl");
        // 调用Service中的方法
        userServiceImpl.test();
    }
}

```

![image-20230417195739859](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417195739859.png)

## IOC创建对象的方式

```
分析IOC是如何创建对象的
```



### 新建模块

选中项目右键 New -> Module

![image-20230417195923967](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417195923967.png)

### 创建User实体类

```java
package com.etjava.model;

public class User {
    private String userName;
 	public User(){
        System.out.println("User类的无参构造方法");
    }
    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public void show(){
        System.out.println("name  = "+userName);
    }
}
```

### 创建Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--注入bean-->
    <bean id="user" class="com.etjava.model.User">
        <!--给bean中的属性注入值 普通属性使用value-->
        <property name="userName" value="Tom"/>
    </bean>

</beans>
```

### 测试

```java
package com.etjava.test;

import com.etjava.model.User;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        // 创建Spring上下文对象
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        // 获取Spring中配置好的User对象
        User user = (User)context.getBean("user");
        // 调用user对象中的show方法
        user.show();
    }
}

```

### 总结

#### 无参构造器

Spring默认是使用无参的构造方法来创建对象

如果我们将无参构造方法去掉之后 运行会直接报错 

![image-20230417202727483](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417202727483.png)

![image-20230417202741966](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417202741966.png)

![image-20230417202805339](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417202805339.png)

#### 有参构造器如何使用

假如我们一定要使用有参的构造方法怎么办？

Spring给我们提供了三种方式可以使用有参构造器

![image-20230417203430929](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417203430929.png)

##### 方式1 下标索引注入属性值

![image-20230417203833484](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417203833484.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--注入bean 使用无参构造方法-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash;给bean中的属性注入值 普通属性使用value&ndash;&gt;
        <property name="userName" value="Tom"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过下标索引方式-->
    <bean id="user" class="com.etjava.model.User">
        <!-- 通过下标索引方式 0表示第一个参数 -->
        <constructor-arg index="0" value="99"/>
    </bean>

</beans>
```

##### 方式2 通过类型匹配有参构造方法

![image-20230417203920213](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417203920213.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--注入bean 使用无参构造方法-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash;给bean中的属性注入值 普通属性使用value&ndash;&gt;
        <property name="userName" value="Tom"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过下标索引方式-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash; 通过下标索引方式 0表示第一个参数 &ndash;&gt;
        <constructor-arg index="0" value="99"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过构造方法中的参数类型
		不建议使用 如果存在多个相同类型的参数无法区分
	-->
    <bean id="user" class="com.etjava.model.User">
        <constructor-arg type="int" value="7500000"/>
    </bean>

</beans>
```

##### 方式3[==常用==] 直接通过参数名方式来设置Bean

![image-20230417204701039](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417204701039.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--注入bean 使用无参构造方法-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash;给bean中的属性注入值 普通属性使用value&ndash;&gt;
        <property name="userName" value="Tom"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过下标索引方式-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash; 通过下标索引方式 0表示第一个参数 &ndash;&gt;
        <constructor-arg index="0" value="99"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过构造方法中的参数类型
		不建议使用 如果存在多个相同类型的参数无法区分
	-->
    <!--<bean id="user" class="com.etjava.model.User">
        <constructor-arg type="int" value="7500000"/>
    </bean>-->

    <!--直接通过参数名来设置-->
    <bean id="user" class="com.etjava.model.User">
        <constructor-arg name="age" value="7500000"/>
    </bean>

</beans>
```

#### bean是什么时候初始化

验证装配到Spring容器中的bean是什么时候初始化的



##### 新建一个User2类 给一个无参构造方法

```java
package com.etjava.model;

public class User2 {
    private String userName;


    public User2(){
        System.out.println("User2类的无参构造方法");
    }
    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public void show(){
        System.out.println("name  = "+userName);
    }
}

```

Spring配置文件中配置User2 bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--注入bean 使用无参构造方法-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash;给bean中的属性注入值 普通属性使用value&ndash;&gt;
        <property name="userName" value="Tom"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过下标索引方式-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash; 通过下标索引方式 0表示第一个参数 &ndash;&gt;
        <constructor-arg index="0" value="99"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过构造方法中的参数类型
		不建议使用 如果存在多个相同类型的参数无法区分
	-->
    <!--<bean id="user" class="com.etjava.model.User">
        <constructor-arg type="int" value="7500000"/>
    </bean>-->

    <!--直接通过参数名来设置-->
    <bean id="user" class="com.etjava.model.User">
        <constructor-arg name="age" value="7500000"/>
    </bean>
    <!--配置User2 bean-->
    <bean id="user2" class="com.etjava.model.User2">
        <property name="userName" value="Jerry"/>
    </bean>

</beans>
```

##### 测试

```java
package com.etjava.test;

import com.etjava.model.User;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        // 创建Spring上下文对象
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        // 获取Spring中配置好的User对象
        User user = (User)context.getBean("user");
        // 调用user对象中的show方法
        user.show();
    }
}

```

![image-20230417205545138](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417205545138.png)

运行结果可以看出 在Spring加载时就会初始化所有配置的bean



#### 验证User是否是单例

```java
package com.etjava.test;

import com.etjava.model.User;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        // 创建Spring上下文对象
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        // 获取Spring中配置好的User对象
        User user = (User)context.getBean("user");
        User user2 = (User)context.getBean("user");
        // 调用user对象中的show方法
        user.show();
        System.out.println(user == user2);
    }
}

```



![image-20230417205700573](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417205700573.png)

## Spring 其他配置

### 新建模块

![image-20230417210434686](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417210434686.png)

#### 创建User实体类

```java
package com.etjava.model;

public class User {
    private String userName;
    public User(){
        System.out.println("User类的无参构造方法");
    }
    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public void show(){
        System.out.println("name  = "+userName);
    }
}

```

### Spring配置文件

#### 别名

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--配置User Bean-->
    <bean id="user" class="com.etjava.model.User">
        <property name="userName" value="Tom"/>
    </bean>
    <!--给user这个bean取一个别名叫做dddd 在getBean时可以通过别名直接获取-->
    <alias name="user" alias="ddddd"/>

</beans>
```

##### 测试

```
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User u1 = (User)context.getBean("user");// 通过bean id="user"获取user对象
        User u2 = (User)context.getBean("ddddd");// 通过别名获取user对象

        System.out.println(u1==u2);
    }
}

```

![image-20230417210930570](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417210930570.png)

#### bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--配置User Bean-->
    <!--<bean id="user" class="com.etjava.model.User">
        <property name="userName" value="Tom"/>
    </bean>-->
    <!--给user这个bean取一个别名叫做dddd 在getBean时可以通过别名直接获取-->
<!--    <alias name="user" alias="ddddd"/>-->

    <!--
        bean 用来配置我们的实体类
        id 是该bean的唯一标识符 相当于实例名(对象名)
        class  bean对象对应的限定名 即 我么写的User对象的全路径
        name 给当前这个bean取别名 可以同时取多个 使用逗号隔开
    -->
    <bean id="user2" class="com.etjava.model.User" name="u1,u2,u3">
        <property name="userName" value="Tom"/>
    </bean>
</beans>

```

##### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User u1 = (User)context.getBean("u1");
        User u2 = (User)context.getBean("u2");

        System.out.println(u1==u2);
    }
}

```

#### import

通常用于团队开发，可以==将多个spring的配置文件合并为一个==

==可以自动合并重名的bean,也可以获取不同的bean==

使用的时候直接使用合并后的那个配置文件即可

复制多个beans.xml 然后创建一个applicationContext.xml

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--引入其他spring配置文件 合并为一个-->
   <import resource="beans.xml"/>
   <import resource="beans2.xml"/>
   <import resource="beans3.xml"/>
</beans>
```

##### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        User u1 = (User)context.getBean("u1");
        User u2 = (User)context.getBean("u2");

        System.out.println(u1==u2);
    }
}

```

![image-20230417212520744](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417212520744.png)

## 依赖注入

新建项目 spring_di

![image-20230417212954907](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417212954907.png)

### 创建User对象

```java
package com.etjava.model;

public class User {
    private String userName;

    public User() {
        System.out.println("无参构造方法");
    }

    public User(String userName) {
        System.out.println("有参构造方法");
        this.userName = userName;
    }

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }
}

```

### 构造器注入

与前边相同 <constructor-arg>

Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--注入bean 使用无参构造方法-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash;给bean中的属性注入值 普通属性使用value&ndash;&gt;
        <property name="userName" value="Tom"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过下标索引方式-->
    <!--<bean id="user" class="com.etjava.model.User">
        &lt;!&ndash; 通过下标索引方式 0表示第一个参数 &ndash;&gt;
        <constructor-arg index="0" value="99"/>
    </bean>-->

    <!--注入bean 使用有参构造方法  通过构造方法中的参数类型
		不建议使用 如果存在多个相同类型的参数无法区分
	-->
    <!--<bean id="user" class="com.etjava.model.User">
        <constructor-arg type="int" value="7500000"/>
    </bean>-->

    <!--直接通过参数名来设置-->
    <bean id="user" class="com.etjava.model.User">
        <constructor-arg name="userName" value="TOM"/>
    </bean>
    <!--配置User2 bean-->
    <bean id="user2" class="com.etjava.model.User">
        <property name="userName" value="Jerry"/>
    </bean>

    <!--给user这个bean取一个别名叫做dddd 在getBean时可以通过别名直接获取-->
    <alias name="user" alias="ddddd"/>

</beans>
```

#### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Object ddddd = context.getBean("user2");
    }
}

```

![image-20230417215443528](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230417215443528.png)

### set注入[重点]

依赖   bean对象的创建依赖于容器

注入 bean对象中的属性由容器注入

#### 复杂类型注入

##### 创建Addresss实体

```java
package com.etjava.model;

public class Address {
    private String addr;

    public String getAddr() {
        return addr;
    }

    public void setAddr(String addr) {
        this.addr = addr;
    }
}

```

##### 创建Student实体

```java
package com.etjava.model;

import java.util.List;
import java.util.Map;
import java.util.Properties;
import java.util.Set;

public class Student {
    private String stuName;
    private Address address;
    private String[] data;
    private List<String> list;
    private Map<String,Object> map;
    private Set<String> set;
    private String nullVal;
    private Properties prop;

    public String getStuName() {
        return stuName;
    }

    public void setStuName(String stuName) {
        this.stuName = stuName;
    }

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    public String[] getData() {
        return data;
    }

    public void setData(String[] data) {
        this.data = data;
    }

    public List<String> getList() {
        return list;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public Map<String, Object> getMap() {
        return map;
    }

    public void setMap(Map<String, Object> map) {
        this.map = map;
    }

    public Set<String> getSet() {
        return set;
    }

    public void setSet(Set<String> set) {
        this.set = set;
    }

    public String getNullVal() {
        return nullVal;
    }

    public void setNullVal(String nullVal) {
        this.nullVal = nullVal;
    }

    public Properties getProp() {
        return prop;
    }

    public void setProp(Properties prop) {
        this.prop = prop;
    }
    @Override
    public String toString() {
        return "Student{" +
                "stuName='" + stuName + '\'' +
                ", address=" + address +
                ", data=" + Arrays.toString(data) +
                ", list=" + list +
                ", map=" + map +
                ", set=" + set +
                ", nullVal='" + nullVal + '\'' +
                ", prop=" + prop +
                '}';
    }
}

```

##### spring配置文件

###### 普通属性值注入

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student.getStuName());
    }
}

```

###### 对象注入

对象注入使用ref引入定义的bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="com.etjava.model.Address"/>

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        <!--对象注入 引用类型使用ref-->
        <property name="address" ref="address"/>
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student.getStuName());
    }
}

```

###### 数组注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="com.etjava.model.Address"/>

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        <!--对象注入 引用类型使用ref-->
        <property name="address" ref="address"/>
        <!--数组注入
            array 表示数组
            value 给数组赋值
        -->
        <property name="data">
            <array>
                <value>Tom</value>
                <value>Jerry</value>
                <value>Andy</value>
            </array>
        </property>
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student);
    }
}

```

###### List注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="com.etjava.model.Address"/>

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        <!--对象注入 引用类型使用ref-->
        <property name="address" ref="address"/>
        <!--数组注入
            array 表示数组
            value 给数组赋值
        -->
        <property name="data">
            <array>
                <value>Tom</value>
                <value>Jerry</value>
                <value>Andy</value>
            </array>
        </property>
        <!--List注入
            与数组注入类似
            使用list标签
            value是给list赋值
        -->
        <property name="list">
            <list>
                <value>吃饭</value>
                <value>睡觉</value>
                <value>打豆豆</value>
            </list>
        </property>
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student);
    }
}

```

![image-20230418205029510](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418205029510.png)

###### Map注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="com.etjava.model.Address"/>

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        <!--对象注入 引用类型使用ref-->
        <property name="address" ref="address"/>
        <!--数组注入
            array 表示数组
            value 给数组赋值
        -->
        <property name="data">
            <array>
                <value>Tom</value>
                <value>Jerry</value>
                <value>Andy</value>
            </array>
        </property>
        <!--List注入
            与数组注入类似
            使用list标签
            value是给list赋值
        -->
        <property name="list">
            <list>
                <value>吃饭</value>
                <value>睡觉</value>
                <value>打豆豆</value>
            </list>
        </property>
        <!--Map注入
            使用map标签注入
            entry 表示注入值 key value形式
            description 添加这个map的描述信息
        -->
        <property name="map">
            <map>
                <description>这是map注入</description>
                <entry key="s1" value="Tom"/>
                <entry key="s2" value="Jerry"/>
                <entry key="s3" value="Andy"/>
            </map>
        </property>
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student);
    }
}

```

![image-20230418205428677](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418205428677.png)

###### Set注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="com.etjava.model.Address"/>

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        <!--对象注入 引用类型使用ref-->
        <property name="address" ref="address"/>
        <!--数组注入
            array 表示数组
            value 给数组赋值
        -->
        <property name="data">
            <array>
                <value>Tom</value>
                <value>Jerry</value>
                <value>Andy</value>
            </array>
        </property>
        <!--List注入
            与数组注入类似
            使用list标签
            value是给list赋值
        -->
        <property name="list">
            <list>
                <value>吃饭</value>
                <value>睡觉</value>
                <value>打豆豆</value>
            </list>
        </property>
        <!--Map注入
            使用map标签注入
            entry 表示注入值 key value形式
            description 添加这个map的描述信息
        -->
        <property name="map">
            <map>
                <description>这是map注入</description>
                <entry key="s1" value="Tom"/>
                <entry key="s2" value="Jerry"/>
                <entry key="s3" value="Andy"/>
            </map>
        </property>
        <!--Set注入-->
        <property name="set">
            <set>
                <value>Haily</value>
                <value>Judy</value>
                <value>Andy</value>
            </set>
        </property>
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student);
    }
}

```

###### null值注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="com.etjava.model.Address"/>

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        <!--对象注入 引用类型使用ref-->
        <property name="address" ref="address"/>
        <!--数组注入
            array 表示数组
            value 给数组赋值
        -->
        <property name="data">
            <array>
                <value>Tom</value>
                <value>Jerry</value>
                <value>Andy</value>
            </array>
        </property>
        <!--List注入
            与数组注入类似
            使用list标签
            value是给list赋值
        -->
        <property name="list">
            <list>
                <value>吃饭</value>
                <value>睡觉</value>
                <value>打豆豆</value>
            </list>
        </property>
        <!--Map注入
            使用map标签注入
            entry 表示注入值 key value形式
            description 添加这个map的描述信息
        -->
        <property name="map">
            <map>
                <description>这是map注入</description>
                <entry key="s1" value="Tom"/>
                <entry key="s2" value="Jerry"/>
                <entry key="s3" value="Andy"/>
            </map>
        </property>
        <!--Set注入-->
        <property name="set">
            <set>
                <value>Haily</value>
                <value>Judy</value>
                <value>Andy</value>
            </set>
        </property>
        <!--null值注入-->
        <property name="nullVal">
            <!--如果是空 直接value为空即可-->
            <!--<value></value>-->
            <!--如果为null 使用null标签即可-->
            <null/>
        </property>
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student);
    }
}

```

![image-20230418220832851](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418220832851.png)



###### Properties注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="address" class="com.etjava.model.Address"/>

    <bean id="student" class="com.etjava.model.Student">
        <!--普通属性值注入 直接使用value赋值-->
        <property name="stuName" value="HCL"/>
        <!--对象注入 引用类型使用ref-->
        <property name="address" ref="address"/>
        <!--数组注入
            array 表示数组
            value 给数组赋值
        -->
        <property name="data">
            <array>
                <value>Tom</value>
                <value>Jerry</value>
                <value>Andy</value>
            </array>
        </property>
        <!--List注入
            与数组注入类似
            使用list标签
            value是给list赋值
        -->
        <property name="list">
            <list>
                <value>吃饭</value>
                <value>睡觉</value>
                <value>打豆豆</value>
            </list>
        </property>
        <!--Map注入
            使用map标签注入
            entry 表示注入值 key value形式
            description 添加这个map的描述信息
        -->
        <property name="map">
            <map>
                <description>这是map注入</description>
                <entry key="s1" value="Tom"/>
                <entry key="s2" value="Jerry"/>
                <entry key="s3" value="Andy"/>
            </map>
        </property>
        <!--Set注入-->
        <property name="set">
            <set>
                <value>Haily</value>
                <value>Judy</value>
                <value>Andy</value>
            </set>
        </property>
        <!--null值注入-->
        <property name="nullVal">
            <!--如果是空 直接value为空即可-->
            <!--<value></value>-->
            <!--如果为null 使用null标签即可-->
            <null/>
        </property>

        <!--
        properties属性的注入
        key是写在 prop标签里面的 value是在prop两个标签中间的
        与map不同  map都是写在entry标签里面的
        -->
        <property name="prop">
            <props>
                <prop key="jdbc.driver">com.mysql.jdbc.Driver</prop>
                <prop key="jdbc.url">http://localhost:3306/db_spring</prop>
            </props>
        </property>
    </bean>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println(student);
    }
}

```

![image-20230418221247808](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418221247808.png)

###### 扩展注入

p命名空间和c命名空间的注入

注意点： p命名和c命名不能直接使用 需要导入约束

```xml
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
```



官方案例

c命名空间

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean name="classic" class="com.example.ExampleBean">
        <property name="email" value="someone@somewhere.com"/>
    </bean>

    <bean name="p-namespace" class="com.example.ExampleBean"
        p:email="someone@somewhere.com"/>
</beans>
```

p命名空间

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:c="http://www.springframework.org/schema/c"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="beanTwo" class="x.y.ThingTwo"/>
    <bean id="beanThree" class="x.y.ThingThree"/>

    <!-- traditional declaration with optional argument names -->
    <bean id="beanOne" class="x.y.ThingOne">
        <constructor-arg name="thingTwo" ref="beanTwo"/>
        <constructor-arg name="thingThree" ref="beanThree"/>
        <constructor-arg name="email" value="something@somewhere.com"/>
    </bean>

    <!-- c-namespace declaration with argument names -->
    <bean id="beanOne" class="x.y.ThingOne" c:thingTwo-ref="beanTwo"
        c:thingThree-ref="beanThree" c:email="something@somewhere.com"/>

</beans>
```



###### P命名空间注入

p命名空间可以直接在注入bean时指定属性值 但是需要单独引入命名空间

![image-20230418222318225](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418222318225.png)

单独创建一个实体类进行测试

Teacher

```java
package com.etjava.model;

public class Teacher {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }



    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
    @Override
    public String toString() {
        return "Teacher{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

spring配置文件中引入p命名空间

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--P命名 可以直接给属性赋值-->
    <bean id="teacher" class="com.etjava.model.Teacher" p:age="21" p:name="Tom"/>

</beans>
```

###### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TeacherTest {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Teacher teacher = context.getBean("teacher", Teacher.class);
        System.out.println(teacher);
    }
}

```

###### C命名空间注入

c命名空间需要构造方法的支持 因此实体类必须有构造方法

```java
package com.etjava.model;

public class Teacher {


    public Teacher(String name, int age) {
        this.name = name;
        this.age = age;
    }

    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }



    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
    @Override
    public String toString() {
        return "Teacher{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

引入c命名空间 使用c命名空间注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--P命名 可以直接给属性赋值-->
    <!--<bean id="teacher" class="com.etjava.model.Teacher" p:age="21" p:name="Tom"/>-->
    <!--C命名空间注入 注入的bean必须有写构造方法-->
    <bean id="teacher" class="com.etjava.model.Teacher" c:age="18" c:name="Jerry" />
</beans>
```

###### 测试

```
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class TeacherTest {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Teacher teacher = context.getBean("teacher", Teacher.class);
        System.out.println(teacher);
    }
}

```

### Bean的作用域

![image-20230418231346912](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418231346912.png)

| Scope                                                        | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [singleton](https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-singleton) | (Default) Scopes a single bean definition to a single object instance for each Spring IoC container. |
| [prototype](https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-prototype) | Scopes a single bean definition to any number of object instances. |
| [request](https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-request) | Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| [session](https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-session) | Scopes a single bean definition to the lifecycle of an HTTP `Session`. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| [application](https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-application) | Scopes a single bean definition to the lifecycle of a `ServletContext`. Only valid in the context of a web-aware Spring `ApplicationContext`. |
| [websocket](https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/web.html#websocket-stomp-websocket-scope) | Scopes a single bean definition to the lifecycle of a `WebSocket`. Only valid in the context of a web-aware Spring `ApplicationContext`. |

#### 创建测试模块

![image-20230418232132371](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418232132371.png)

##### 添加Teacher实体类

```java
package com.etjava;

public class Teacher {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

#### singleton 单例

![image-20230418231704698](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418231704698.png)

默认就是单例的 我们也可以显示的给bean添加一个单例

##### spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--scope 指定bean的作用域 默认就是singleton 单例的-->
    <bean id="teacher" class="com.etjava.Teacher"  scope="singleton">
        <property name="name" value="Tom"/>
    </bean>
</beans>
```

##### 测试

```java
package com.etjava;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Teacher teacher = context.getBean("teacher", Teacher.class);
        Teacher teacher2 = context.getBean("teacher", Teacher.class);
        System.out.println(teacher==teacher2);
    }
}

```

![image-20230418232844749](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418232844749.png)

#### prototype 原型模式

原型模式与单例模式相反 每个对象都有单独的实例

![image-20230418233115374](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418233115374.png)

##### spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--scope 指定bean的作用域 默认就是singleton 单例的-->
    <!--<bean id="teacher" class="com.etjava.Teacher"  scope="singleton">
        <property name="name" value="Tom"/>
    </bean>-->
    <!--原型模式 每个bean都有一个实例 与单例相反 每次获取时都会产生一个新对象-->
    <bean id="teacher" class="com.etjava.Teacher"  scope="prototype">
        <property name="name" value="Tom"/>
    </bean>
</beans>
```

##### 测试

```java
package com.etjava;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Teacher teacher = context.getBean("teacher", Teacher.class);
        Teacher teacher2 = context.getBean("teacher", Teacher.class);
        System.out.println(teacher==teacher2);
    }
}

```

![image-20230418233305878](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418233305878.png)

#### request、session、application

这些只能在web开发环境中使用

```
<web-app>
    ...
    <filter>
        <filter-name>requestContextFilter</filter-name>
        <filter-class>org.springframework.web.filter.RequestContextFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>requestContextFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ...
</web-app>

<bean id="userPreferences" class="com.something.UserPreferences" scope="request"/>
```

## 自动装配Bean

```
自动装配bean 其实指的就是扫描bean 然后自动加载到IOC容器中
spring会在上下文环境中自动查找，并自动给bean配置属性（这个属性都是默认值）
在Spring中提供了三种Bean的装配方式
    1 xml中显示的配置 就是我们上边手动写的
    2 隐士的装配Bean 【重点】
    3 通过配置类显示配置(后边讲)
```

### 新建模块

![image-20230418234520705](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230418234520705.png)

### 新建实体类

既然是自动装配 我们可以写多个实体类(bean) 测试

Cat

```java
package com.etjava.model;

public class Cat {
    public void eat(){
        System.out.println("猫吃鱼~");
    }
}

```



Dog

```java
package com.etjava.model;

public class Dog {
    public void eat(){
        System.out.println("狗吃肉~");
    }
}

```

User

```java
package com.etjava.model;

public class User {
    private Cat cat;
    private Dog dog;
    private String name;

    public Cat getCat() {
        return cat;
    }

    public void setCat(Cat cat) {
        this.cat = cat;
    }

    public Dog getDog() {
        return dog;
    }

    public void setDog(Dog dog) {
        this.dog = dog;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "cat=" + cat +
                ", dog=" + dog +
                ", name='" + name + '\'' +
                '}';
    }
}

```

### XML中显示装配

#### Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

   <!--显示装配
    需要讲所有的bean手动的写出来
   -->
    <bean id="dog" class="com.etjava.model.Dog" />
    <bean id="cat" class="com.etjava.model.Cat" />
    <bean id="user" class="com.etjava.model.User">
        <property name="name" value="Andy"/>
        <property name="cat" ref="cat"/>
        <property name="dog" ref="dog"/>
    </bean>



</beans>
```

#### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user = context.getBean("user", User.class);
        user.getCat().eat();
        user.getDog().eat();
    }
}

```

![image-20230419000407659](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419000407659.png)

### 隐士装配

#### autowire="byName"

spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="dog" class="com.etjava.model.Dog" />
    <bean id="cat" class="com.etjava.model.Cat" />
    <!--显示装配
      需要讲所有的bean手动的写出来
     -->
    <!--<bean id="user" class="com.etjava.model.User">
        <property name="name" value="Andy"/>
        <property name="cat" ref="cat"/>
        <property name="dog" ref="dog"/>
    </bean>-->
      <!--自动装配
       byName 根据bean的id来装配
                会自动在spring上下文中查找和自己对象set后面的值对应的 bean的id
                这里的自己对象指的是user 会去user中查找setDog  setCat
            注意 id值要与类名保持一直 且 首字母小写
  		-->
    <bean id="user" class="com.etjava.model.User" autowire="byName">
        <property name="name" value="Andy"/>
    </bean>



</beans>
```

##### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user = context.getBean("user", User.class);
        user.getCat().eat();
        user.getDog().eat();
    }
}

```

![image-20230419001017443](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419001017443.png)



#### autowire="byType"

spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">


    <bean id="dog" class="com.etjava.model.Dog" />
    <bean id="cat23" class="com.etjava.model.Cat" />
    <!--显示装配
      需要讲所有的bean手动的写出来
     -->
    <!--<bean id="user" class="com.etjava.model.User">
        <property name="name" value="Andy"/>
        <property name="cat" ref="cat"/>
        <property name="dog" ref="dog"/>
    </bean>-->
    <!--自动装配
        byName 根据bean的id来装配
                会自动在spring上下文中查找和自己对象set后面的值对应的 bean的id
                这里的自己对象指的是user 会去user中查找属性名叫做 dog,cat
            注意 id值要与类名保持一直 且 首字母小写
   -->
    <!--<bean id="user" class="com.etjava.model.User" autowire="byName">
        <property name="name" value="Andy"/>
    </bean>-->

    <!--自动装配
       byName 根据bean的id来装配
                会自动在spring上下文中查找和自己对象中类型相同的bean
                这里的自己对象指的是user 会去user中查找属性为dog  cat
                注意 byType找的是属性的类型 因此不会关注bean的id
  -->
    <bean id="user" class="com.etjava.model.User" autowire="byType">
        <property name="name" value="Andy"/>
    </bean>



</beans>
```

##### 测试

```java
package com.etjava.model;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user = context.getBean("user", User.class);
        user.getCat().eat();
        user.getDog().eat();
    }
}

```

![image-20230419001735017](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419001735017.png)

```
小结
byName 需要保证所有bean的id唯一，并且该Bean需要和自动注入的属性名保持一致
byType 需要保证所有bean的class唯一 并且该Bean需要和自动注入的属性类型保持一致
```

![image-20230419001948971](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419001948971.png)

### 注解装配

![image-20230419064236772](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419064236772.png)

使用注解注意事项：

导入context约束并开启注解

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>
	配置bean 但不需要配置bean的属性了
</beans>
```



#### 新建模块

![image-20230419200509638](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419200509638.png)

#### 创建实体类

学生、老师、班级  关系：班级里面包含老师和学生

##### Student

```java
package com.etjava.model;

public class Student {
   public void study(){
       System.out.println("学生学习的方法");
   }
}

```

Teacher

```java
package com.etjava.model;

public class Teacher {
    public void teach(){
        System.out.println("老师教学的方法");
    }
}

```

Clazz

```java
package com.etjava.model;

public class Clazz {

    private String className;
    private Student stu;
    private Teacher teacher;

    public String getClassName() {
        return className;
    }

    public void setClassName(String className) {
        this.className = className;
    }

    public Student getStu() {
        return stu;
    }

    public void setStu(Student stu) {
        this.stu = stu;
    }

    public Teacher getTeacher() {
        return teacher;
    }

    public void setTeacher(Teacher teacher) {
        this.teacher = teacher;
    }
}

```

#### @Autowired

==Autowired可以在属性上使用 也可以在set方法上使用==

使用Autowired注解前提是 bean中的属性必须在spring的IOC容器中存在

##### 属性上使用注解

###### spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启注解-->
    <context:annotation-config/>

    <!--注入bean 但不需要注入bean的属性了 采用注解方式实现属性的注入-->
    <bean id="student" class="com.etjava.model.Student"/>
    <bean id="teacher" class="com.etjava.model.Teacher"/>
    <bean id="clazz" class="com.etjava.model.Clazz"/>

</beans>
```

###### 实体类中使用注解

```java
package com.etjava.model;

import org.springframework.beans.factory.annotation.Autowired;

public class Clazz {

    private String className;
    @Autowired // 对应的是spring配置文件中配置好的bean
    private Student stu;
    @Autowired
    private Teacher teacher;

    public String getClassName() {
        return className;
    }

    public void setClassName(String className) {
        this.className = className;
    }

    public Student getStu() {
        return stu;
    }

    public void setStu(Student stu) {
        this.stu = stu;
    }

    public Teacher getTeacher() {
        return teacher;
    }

    public void setTeacher(Teacher teacher) {
        this.teacher = teacher;
    }
}

```

###### 测试

```java
package com.etjava;

import com.etjava.model.Clazz;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Clazz clazz = context.getBean("clazz", Clazz.class);
        clazz.getTeacher().teach();
        clazz.getStu().study();

    }
}

```

##### 在set方法上使用

###### spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启注解-->
    <context:annotation-config/>

    <!--注入bean 但不需要注入bean的属性了 采用注解方式实现属性的注入-->
    <bean id="student" class="com.etjava.model.Student"/>
    <bean id="teacher" class="com.etjava.model.Teacher"/>
    <bean id="clazz" class="com.etjava.model.Clazz"/>

</beans>
```

###### Clazz set方法上加注解

```java
package com.etjava.model;

import org.springframework.beans.factory.annotation.Autowired;

public class Clazz {

    private String className;

    private Student stu;

    private Teacher teacher;

    public String getClassName() {
        return className;
    }

    public void setClassName(String className) {
        this.className = className;
    }

    public Student getStu() {
        return stu;
    }
    @Autowired // 对应的是spring配置文件中配置好的bean
    public void setStu(Student stu) {
        this.stu = stu;
    }

    public Teacher getTeacher() {
        return teacher;
    }
    @Autowired
    public void setTeacher(Teacher teacher) {
        this.teacher = teacher;
    }
}

```

###### 测试

```java
package com.etjava;

import com.etjava.model.Clazz;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Clazz clazz = context.getBean("clazz", Clazz.class);
        clazz.getTeacher().teach();
        clazz.getStu().study();

    }
}

```

##### 扩展

```
@Nullable 表示该属性值可以为null
@Autowired(required = false) required=false 表示该属性可以为null
如果@Autowired自动注入的属性比较复杂 无法通过一个注解(@Autowired)完成时 我们可以使用@Qualifier(value="xx")去配合@Autowired使用 指定一个唯一的bean对象注入
```

###### Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启注解-->
    <context:annotation-config/>

    <!--注入bean 但不需要注入bean的属性了 采用注解方式实现属性的注入
		有多个bean时可以通过@Qualifier指定需要注入的bean
	-->
    <bean id="student2" class="com.etjava.model.Student"/>
    <bean id="student22" class="com.etjava.model.Student"/>
    <bean id="teacher22" class="com.etjava.model.Teacher"/>
    <bean id="clazz" class="com.etjava.model.Clazz"/>

</beans>
```

###### Clazz使用注解注入属性

```java
package com.etjava.model;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.lang.Nullable;

public class Clazz {

    private String className;
    // 对应的是spring配置文件中配置好的bean
    // 如果我们设置了Autowired属性required值为false  表示该属性可以为null
    @Autowired(required = false)
    @Qualifier(value = "student2")// 表示去IOC中查找对应名字的bean
    private Student stu;
    @Autowired // 对应的是spring配置文件中配置好的bean
    private Teacher teacher;

    // 添加了Nullable 注解 表示该参数可以为null
    public Clazz(@Nullable  String className) {
        this.className = className;
    }

    public String getClassName() {
        return className;
    }

    public void setClassName(String className) {
        this.className = className;
    }

    public Student getStu() {
        return stu;
    }

    public void setStu(Student stu) {
        this.stu = stu;
    }

    public Teacher getTeacher() {
        return teacher;
    }
    public void setTeacher(Teacher teacher) {
        this.teacher = teacher;
    }
}

```

###### 测试

```java
package com.etjava;

import com.etjava.model.Clazz;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Clazz clazz = context.getBean("clazz", Clazz.class);
        clazz.getTeacher().teach();
        clazz.getStu().study();

    }
}

```

#### @Resource

该注解是JDK提供的 兼容了@Autowired 当找不到名字时则按类型查找

先byName 如果找不到在byType 两个如果都找不到则抛出异常

##### spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    <!--开启注解-->
    <context:annotation-config/>

    <!--注入bean 但不需要注入bean的属性了 采用注解方式实现属性的注入-->
    <bean id="stu1" class="com.etjava.model.Student"/>
    <bean id="stu2" class="com.etjava.model.Student"/>
    <bean id="teacher22" class="com.etjava.model.Teacher"/>
    <bean id="clazz" class="com.etjava.model.Clazz"/>

</beans>
```

##### Clazz中使用resource注解

```java
package com.etjava.model;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.lang.Nullable;

import javax.annotation.Resource;

public class Clazz {

    private String className;
    // 对应的是spring配置文件中配置好的bean
    // 如果我们设置了Autowired属性required值为false  表示该属性可以为null
//    @Autowired(required = false)
//    @Qualifier(value = "student2")// 表示去IOC中查找对应名字的bean
    @Resource(name = "stu2")// 指定IOC配置的bean
    private Student stu;
    @Resource
    private Teacher teacher;

    // 添加了Nullable 注解 表示该参数可以为null
    public Clazz(@Nullable  String className) {
        this.className = className;
    }

    public String getClassName() {
        return className;
    }

    public void setClassName(String className) {
        this.className = className;
    }

    public Student getStu() {
        return stu;
    }

    public void setStu(Student stu) {
        this.stu = stu;
    }

    public Teacher getTeacher() {
        return teacher;
    }
    public void setTeacher(Teacher teacher) {
        this.teacher = teacher;
    }
}

```

##### 测试

```java
package com.etjava;

import com.etjava.model.Clazz;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Clazz clazz = context.getBean("clazz", Clazz.class);
        clazz.getTeacher().teach();
        clazz.getStu().study();

    }
}

```

小结

```
@Resource & @Autowired区别
都是用来自动注入属性的，都可以应用于属性字段上
@Autowired 通过byType方式实现 必须要求这个而对象在Spring的IOC容器中存在【常用】
@Resource 默认通过byName方式实现 如果找不到则通过byType实现，如果两个都找不到则抛出异常

执行顺序不同  @Autowired byType实现，@Resource默认byName实现
```

### 使用注解开发

```
在spring4之后 要使用注解开发业务 必须保证aop的依赖包导入了
```

![image-20230419210346834](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419210346834.png)





#### 新建模块

![image-20230419211507567](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419211507567.png)

#### @Component注解 【Bean注入】

该注解表示这个实体类已经被Spring管理了，在Spring的配置文件中不需要配置 但需要开启component扫描

##### Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!--扫描包  该包下的注解就会生效-->
    <context:component-scan base-package="com.etjava"/>
    <!--开启注解-->
    <context:annotation-config/>




</beans>
```

##### 新建实体类

```java
package com.etjava.model;

import org.springframework.stereotype.Component;

// Component 定义为组件的注解
// 等价于 <bean id="user" class="com.etjava.model.User"/>
@Component
public class User {
    public String name = "ET";
}
```

##### 测试

```java
package com.etjava.test;

import com.etjava.model.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user = context.getBean("user", User.class);
        System.out.println(user.name);
    }
}

```

#### @Value注解 【属性注入】

该注解是用来给属性注入值的

需要结合上述案例中的@Component注解使用

##### User实体

```java
package com.etjava.model;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

// Component 定义为组件的注解
// 等价于 <bean id="user" class="com.etjava.model.User"/>
@Component
public class User {
    @Value("Tom")// 给属性注入值,优先级低于直接赋值 但它会覆盖掉之前的值
    public String name = "ET";
}

```

##### Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!--扫描包  该包下的注解就会生效-->
    <context:component-scan base-package="com.etjava"/>
    <!--开启注解-->
    <context:annotation-config/>




</beans>
```

##### 测试

```java
package com.etjava.test;

import com.etjava.model.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user = context.getBean("user", User.class);
        System.out.println(user.name);
    }
}

```

#### 衍生注解

```
@Component 有几个衍生注解 通常我们在不同的分层中使用不同的注解
	dao - @Repository
	service - @Service
	Controller - @Controller
以上这四个注解功能都是一样的 都是将我们写的类注册到Spring容器中 装配成Bean
```

演示demo 无实际效果 只是演示注解在每一层的使用

```java
controller层
import org.springframework.stereotype.Controller;
@Controller
public class UserController {
}

service层
import org.springframework.stereotype.Service;
@Service
public class UserService {
}

dao层
import org.springframework.stereotype.Repository;
@Repository
public class UserDao {
}    
```

#### 自动装配

```java
自动装配指的就是@Autowirt注解
    @Autowirte 自动给bean注入属性值 前提是要注入的属性必须由Spring管理的bean
    	如果Autowire不能确定需要注入的属性是哪个(Spring的IOC中存在多个)
    	则需要通过@Qualifier(value="bean id")指定要注入的bean
    @Nullable 表示被标记的属性或参数可以为null
    @Resource	自动装配 默认byName 找不到再根据类型查找(byType)
```

#### 注解配置作用域

@Scope需要配合@Component或与之同级的组件注解使用

@Scope可以指定bean的作用域 例如单例，原型等

```java
package com.etjava.model;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;

// Component 定义为组件的注解
// 等价于 <bean id="user" class="com.etjava.model.User"/>
@Component
@Scope("singleton")// prototype 原型模式  singeton单例模式
public class User {
    @Value("Tom")// 给属性注入值,优先级低于直接赋值 但它会覆盖掉之前的值
    public String name = "ET";
}

```

Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!--扫描包  该包下的注解就会生效-->
    <context:component-scan base-package="com.etjava"/>
    <!--开启注解-->
    <context:annotation-config/>




</beans>
```

测试

```java
package com.etjava.test;

import com.etjava.model.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Test {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user = context.getBean("user", User.class);
        User user2 = context.getBean("user", User.class);
        System.out.println(user==user2);
    }
}

```

![image-20230419214945439](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419214945439.png)





#### 小结

```
xml可以配置任何一切bean,适用于任何场合 且维护简单方便
注解 不是自己的类无法使用注解 维护相对复杂

xml于注解 最佳实践
	xml只负责管理bean
	注解只负责bean中属性注入

注意：使用注解 必须要确保注解生效
	在Spring中引入约束并开启注解
	xmlns:context="http://www.springframework.org/schema/context"
	
	http://www.springframework.org/schema/context
	
	
	<!--扫描包  该包下的注解就会生效-->
    <context:component-scan base-package="com.etjava"/>
    <!--开启注解-->
    <context:annotation-config/>
```

## Configuration替代Spring配置文件

javaConfig是spring的一个子项目 在Spring4之后作为spring的一个核心功能

其作用是用来替代xml方式配置bean

### 新建项目

...

### 新建实体类

```java
package com.etjava.model;

import org.springframework.beans.factory.annotation.Value;
// 这里不需要在使用@Component注解来注入到Spring容器中
// 因为使用@Configuration进行配置bean时 通过@Bean方式作为属性去引用了
public class User {
    private String name;

    public String getName() {
        return name;
    }

    @Value("Tom")// 给name赋值 @Value还可以写在属性上
    public void setName(String name) {
        this.name = name;
    }
}

```

### 创建config配置类

```java
package com.etjava.config;

import com.etjava.model.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;


/*
    @Configuration 代表Spring的配置类 与applicationContext.xml作用相同
       @Configuration也会被注册到Spring容器中，因为它本身也是一个@Component

    @ComponentScan("com.etjava.model")// 扫描包 将包下的所有类注册到spring容器中

    @Component
    public @interface Configuration{}
 */
@Configuration
@ComponentScan("com.etjava.model")// 扫描包 将包下的所有类注册到spring容器中
@Import(AppConfig2.class) // 引入其他配置类 相当于spring的xml中的<import resource="beans.xml"/>
public class AppConfig {

    /*
    @Bean 注册一个bean,相当于 <bean id="user" class="xxx">
        这个方法的名字相当于bean标签的id
        这个方法的返回值 相当于bean的class属性
     */
    @Bean
    public User user(){
        return new User();// 相当于需要注入到Spring中的对象
    }
}

```

### 被引入的配置类

```java
package com.etjava.config;

import com.etjava.model.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;


/*
    @Configuration 代表Spring的配置类 与applicationContext.xml作用相同
       @Configuration也会被注册到Spring容器中，因为它本身也是一个@Component

    @ComponentScan("com.etjava.model")// 扫描包 将包下的所有类注册到spring容器中

    @Component
    public @interface Configuration{}
 */
@Configuration
@ComponentScan("com.etjava.model")// 扫描包 将包下的所有类注册到spring容器中
public class AppConfig2 {

    /*
    @Bean 注册一个bean,相当于 <bean id="user" class="xxx">
        这个方法的名字相当于bean标签的id
        这个方法的返回值 相当于bean的class属性
     */
    @Bean
    public User user2(){
        System.out.println("AppConfig2......");
        return new User();// 相当于需要注入到Spring中的对象
    }
}

```

### 测试

```java
package com.etjava.test;

import com.etjava.config.AppConfig;
import com.etjava.model.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Test {
    public static void main(String[] args) {
        // 如果使用了配置类的方式 替代spring的配置文件 那么我们只能通过AnnotationConfig上下文获取spring容器
        // 通过配置类的class对象加载到配置类
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        // 获取的bean 是AppConfig中对应的方法名
        User user = context.getBean("user", User.class);
        System.out.println(user.getName());
    }
}

```

![image-20230419230631361](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419230631361.png)



### 小结

```
我们新建一个类然后在类上添加@Configuration注解 那么这个类就成为了Sprign的配置类
我们可以像配置spring的xml文件一样来配置我们的bean

配置类中常用的注解
	@Configuration 代表Spring的配置类 与applicationContext.xml作用相同
      它也会被注册到Spring容器中，因为它本身也是一个@Component
    @ComponentScan("com.etjava.model")// 扫描包 将包下的所有类注册到spring容器中
    @Import(AppConfig2.class) // 引入其他配置类 
    		相当于spring的xml中的<import resource="beans.xml"/>
    		
既然没有spring的xml配置文件了 我们的Bean要怎么注入属性呢？
	在我们的Bean中可以通过@Component标注这是一个spring管理的bean 其实也可以不用加这个注解
	因为我们在配置类中注入bean的时候使用的@Bean就会帮我们去动态生成了
	@Value注解 给属性注入值 

xml方式获取spring上下文对象 ClassPathXmlApplicationContext("beans.xml")
注解方式获取Spring上下文对象 AnnotationConfigApplicationContext(AppConfig.class)
      
```

Spring的IOC核心理念

所有的Bean都需要注册到Spring中

所有的Bean都需要通过IOC容器去获取

在容器中获取到的Bean就是一个对象 可以直接调用对象中的属性和方法

## 代理模式

```
什么是代理  例如中介
为什么要学习代理模式，因为SpringAOP的底层实现采用的就是代理模式
代理模式的分类
	静态代理和动态代理
代理模式如何理解
	例如 我们去租房子 在没有房屋中介之前 我们是直接找房主，而随着时间的演化 房主只想把房子租出去拿到租金即可，不想管理房客的任何事情，此时就衍生出一个新的行业 叫做房屋中介 房屋中介对应到我们这边就是代理模式
	中介拿到房源 然后把房子卖给我们 那么我们与房主之间没有任何关联 但我们又都有相同的目的 房屋

```

![image-20230419232732849](C:\Users\etjav\AppData\Roaming\Typora\typora-user-images\image-20230419232732849.png)



### 静态代理

```
角色分析
	目的(抽象角色) 通常会使用接口或抽象类来解决
	真实角色 被代理的角色
	代理角色 代理真实的角色
			代理了真实的角色后 我们通常会做一些附属操作
	客户 访问代理的人
	
```

















































































官方文档 1.4

https://docs.spring.io/spring-framework/docs/5.2.23.RELEASE/spring-framework-reference/core.html#beans-c-namespace



