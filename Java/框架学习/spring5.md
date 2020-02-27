

### 一、历史

基于interface21上开发

### 二、优点

![image-20191209010318262](/Users/mecewe/Library/Application Support/typora-user-images/image-20191209010318262.png)

![image-20191209010612670](/Users/mecewe/Library/Application Support/typora-user-images/image-20191209010612670.png)

### 三、组成

七大模块组成

![image-20191209010736958](/Users/mecewe/Library/Application Support/typora-user-images/image-20191209010736958.png)

![image-20191209124714489](/Users/mecewe/Library/Application Support/typora-user-images/image-20191209124714489.png)

![image-20191209143939623](/Users/mecewe/Library/Application Support/typora-user-images/image-20191209143939623.png)

### 四、IOC实现

1、创建对象方式

- 使用无参构造创建对象，默认！

- 使用有参构造创建对象

  - 下标赋值

    ```xml
    <bean id="exampleBean" class="examples.ExampleBean">
        <constructor-arg index="0" value="7500000"/>
        <constructor-arg index="1" value="42"/>
    </bean>
    ```

  - 通过类型赋值(不推荐)

    ```xml
    <bean id="exampleBean" class="examples.ExampleBean">
        <constructor-arg type="int" value="7500000"/>
        <constructor-arg type="java.lang.String" value="42"/>
    </bean>
    ```

  - 通过参数名赋值（主要）

    ```xml
    <bean id="exampleBean" class="examples.ExampleBean">
        <constructor-arg name="years" value="7500000"/>
        <constructor-arg name="ultimateAnswer" value="42"/>
    </bean>
    ```

### 五、spring配置

#### 5.1 Alias 别名

> 如果添加了别名，也能通过别名获取到这个对象

```xml
<alias name="user" alias="user2"/>
```

#### 5.2 Bean的配置

>id：bean的唯一标识符，也就是我们学的对象名
>
>class：bean对象所对应的全限定名：包名+类型
>
>name：也是别名，而且name可以同时取多个别名

```xml
<bean id="user" class="com.mecewe.proj.User" name="u1 u2,u3;u4">
		<property name="name" value="ohayoo" /> 
</bean>      
```

#### 5.3 import

![image-20191209151758170](/Users/mecewe/Library/Application Support/typora-user-images/image-20191209151758170.png)

### 六、依赖注入

#### 6.1 构造器注入

前面已经提到

#### 6.2 set方式注入(重点)

- 依赖注入：set注入
  - 依赖：bean对象的创建依赖于容器
  - 注入：bean对象中的所有属性，由容器注入

#### 6.3 拓展方式注入

- 我们可以使用p命令空间和c命令空间进行注入

  - p命名和c命名空间不能直接使用，需要导入xml约束

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:p="http://www.springframework.org/schema/p"
         xmlns:c="http://www.springframework.org/schema/c"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd">
    
      <bean id="user" class="com.mecewe.proj.User" p:name="alohaha" p:age="123"/>
      <bean id="user2" class="com.mecewe.proj.User" c:age="21" c:name="qwe"/>
  
  </beans>
  ```

### 七、Beans的作用域

![image-20191211111339641](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211111339641.png)

#### 7.1 单例模式(spring默认机制)

```xml
<bean id="user2" class="com.mecewe.proj.User" c:age="21" c:name="qwe" scope="singleton"/>
```

#### 7.2 原型模式

> 每次从容器中get的时候，都会产生一个新对象

```xml
<bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
```

#### 7.3 其余的request、session、application

> 这些只能在web开发中使用到！

### 八、自动装配

- 自动装配是spring满足bean依赖的一种方式
- Spring会在上下文自动寻找，并给bean装配属性

#### 8.1 ByName自动装配

```xml
<bean id="person" class="com.mecewe.Person" autowire="byName">
		<property name="name" value="ohayoo" />
</bean>
```

#### 8.2 ByType自动装配

```xml
<bean id="person" class="com.mecewe.Person" autowire="byType">
  	<property name="name" value="ohayoo" />
</bean>
```

#### 8.3 小结

![image-20191211143237790](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211143237790.png)

#### 8.4 使用注解实现自动装配

jdk1.5开始支持注解，Spring2.5开始支持注解。

使用注解须知：

1、导入约束：context约束

2、配置注解的支持：**<context:annotation-config/>** 

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

</beans>
```

- @Autowired  可追加一个注解@Qualifier(value = " ")

  ![image-20191211150052797](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211150052797.png)

- @Resource 可加（name = " "）

  也能自动装配，是java的原生代码，更加强大

  先通过名字扫描，再扫描唯一的类

  ##### @Autowired和@Resource的区别

  - 同

    - 都是自动装配的，都可以放在属性字段上

  - 异

    - @Autowired 默认通过byType的方式实现，而且必须要求这个对象存在【常用】

      如果类型不唯一，可追加@Qualifier(value = " ") 来通过byName实现

    - @Resource 默认通过byName的方式实现，如果找不到名字，则通过byType实现！如果两个都找不到的情况下，就报错！【常用】

    - 执行顺序不同：@Autowired通过byType的方式实现。@Resource默认通过byname的方式实现。
    
    - #### 其他参考：@Autowired和@Resource两个注解的区别：
    
      1、@Autowired默认按照byType方式进行bean匹配，@Resource默认按照byName方式进行bean匹配
      2、**@Autowired是Spring的注解**，**@Resource是J2EE的注解**，根据导入注解的的包名就可以知晓。
      Spring属于第三方的，J2EE是Java自己的东西。因此，建议使用@Resource注解，以减少代码和Spring之间的耦合。

### 九、使用注解开发

#### 9.1 Bean：@Component @Repository @Service @Controller

- @Component  组件，放在类上，说明这个类被Spring管理了，就是bean！

  等价于 <bean id="user" class="com.mecewe.proj.User" />

  @Component **有几个衍生注解**，我们在web开发中，会按照mvc三层架构分层

  - dao 【@Repository】
  - service 【@Service】
  - controller 【@Controller】

  **这四个注解功能都是一样的**，都是代表将某个类注册到Spring中，装配Bean！

#### 9.2 属性注入 @Value

- @Value("123")  类的属性赋值 在属性上或者set方法

  等价于<property name="name" value="123" />

#### 9.3 自动装配 

![image-20191211162004756](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211162004756.png)

#### 9.4 作用域

@Scope("prototype") 类的作用域prototype、singleton、request、session

![image-20191211162512754](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211162512754.png)

#### 9.5 小结

![image-20191211162841265](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211162841265.png)

![image-20191211162930390](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211162930390.png)



- @Configuration 
  - 这个也会注册到容器中，本来就是一个@Component 
  - 代表一个配置类，等价于beans.xml

- @Bean
  -  注册一个bean，就相当于我们之前写了一个bean标签
  - 方法名就相当于bean的id属性
  - 这个方法的返回值，就相当于就相当于bean标签中的class属性

```java
@Configuration

public class MyConfig {

    @Bean
    public User getUser(){
        return new User();
    }
}
```

⚠️**注意**：完全使用了配置类方式去做，我们就只能通过AnnotationConfig上下文来获取容器，通过配置类的class对象加载。

```java
ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
User user = (User) context.getBean("getUser");
System.out.println(user.getName());
```

### 十、代理模式

SpringAOP的底层

- 静态代理
- 动态代理

#### 10.1 静态代理

![image-20191211203609913](/Users/mecewe/Library/Application Support/typora-user-images/image-20191211203609913.png)

- 好处
  - 可以使真实角色的操作更加纯粹，不用去关注一些公共的业务
  - 公共也就交给代理角色，实现业务的分工
  - 公共业务发生扩展的时候，方便集中管理
- 坏处
  - 一个真实的角色就会产生一个代理角色，代码量会翻倍，降低效率

#### 10.2 动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的，不是我们直接写好的
- 动态代理分为两大类，基于接口的动态代理和基于类的动态代理
  - 基于接口 --- JDK动态代理
  - 基于类：cglib
  - java字节码实现：javasit

需要了解两个类：Proxy：代理、InvocationHandler：调用处理程序

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191211215955623.png" alt="image-20191211215955623" style="zoom:50%;" />

动态代理好处

- 可以使真实角色的操作更加纯粹，不用去关注一些公共的业务
- 公共也就交给代理角色，实现业务的分工
- 公共业务发生扩展的时候，方便集中管理
- 一个动态代理类代理的是一个接口，一般就是对应的一类业务
- 一个动态代理类可以代理多个类，只要实现了多个接口即可

### 十一、AOP

#### 11.1 概念

AOP(Aspect Oriented Programming) 意为：面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。AOP是OOP的延续，是函数式编程的一种衍生范型。利用AOP可以对对各个部分进行隔离，从而使得业务逻辑个部分之间的耦合度降低，提高程序的可重用性，同时提高开发的效率。

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191212101029515.png" alt="image-20191212101029515" style="zoom:40%;" />

#### 11.2 AOP在Spring中的作用

![image-20191212103318307](/Users/mecewe/Library/Application Support/typora-user-images/image-20191212103318307.png)

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191212103434332.png" alt="image-20191212103434332" style="zoom:33%;" />

Spring支持的5种类型的advice

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191212103635286.png" alt="image-20191212103635286" style="zoom:35%;" />

##### 方式一：使用spring的API接口

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

<!--    注册bean-->
    <bean id="userService" class="com.mecewe.service.UserServiceImpl"/>
    <bean id="log" class="com.mecewe.log.Log"/>
    <bean id="afterLog" class="com.mecewe.log.AfterLog"/>

<!--    方式一：使用原生Spring API接口-->
<!--    配置aop，需要导入原生aop约束-->
    <aop:config>
<!--        切入点：expression：表达式：execution(要执行的位置 * * * * *)-->
        <aop:pointcut id="point" expression="execution(* com.mecewe.service.UserServiceImpl.*(..))"/>

<!--        执行环绕增加-->
        <aop:advisor advice-ref="log" pointcut-ref="point"/>
        <aop:advisor advice-ref="afterLog" pointcut-ref="point"/>
    </aop:config>
</beans>
```

##### 方式二：自定义类来实现aop

```xml
<bean id="diy" class="com.mecewe.diy.DiyPointCut"/>

<aop:config>
  <aop:aspect ref="diy">
    <aop:pointcut id="point" expression="execution(* com.mecewe.service.UserServiceImpl.*(..))"/>

    <aop:before method="before" pointcut-ref="point"/>
    <aop:after method="after" pointcut-ref="point"/>
  </aop:aspect>
</aop:config>
```

##### 方式三：使用注解实现

- bean配置

```xml
<!--    方式三-->
    <bean id="pointCut" class="com.mecewe.diy.AnnotationPointCut"/>
<!--    开启注解支持！ JDK（默认，proxy-target-class="false"） cglib（proxy-target-class="true")-->
    <aop:aspectj-autoproxy proxy-target-class="false"/>
```

- java代码

```java
@Aspect
public class AnnotationPointCut {

    @Before("execution(* com.mecewe.service.UserServiceImpl.*(..))")
    public void before(){
        System.out.println("-------执行前-------");
    }

    @After("execution(* com.mecewe.service.UserServiceImpl.*(..))")
    public void after(){
        System.out.println("-------执行后-------");
    }

    @Around("execution(* com.mecewe.service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println(".......环绕前.......");
        Signature signature = pjp.getSignature();
        System.out.println(signature);
        Object proceed = pjp.proceed();
        System.out.println(".......环绕后.......");
        System.out.println(proceed);
    }
}
```

### 十二、mybatis-spring

#### 12.1 步骤

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191212211922438.png" alt="image-20191212211922438" style="zoom:45%;" />

#### 12.2 配置事例一「主要」

##### **spring-mybatis.xml配置**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

<!--    Datasource:使用spring的数据源替换Mybatis的配置 c3p0 dbcp druid-->
<!--    这里使用Spring提供的JDBC：org.springframework.jdbc.datasource-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://122.51.99.239:3306/demo"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
    </bean>

<!--    SqlSessionFactoryBean-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/mecewe/mapper/*.xml"/>
    </bean>

<!--    SqlSessionTemplate-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
<!--        只能使用构造器注入sqlSessionFactory，因为没有set方法-->
        <constructor-arg index="0" ref="sqlSessionFactory"/>
    </bean>

<!--    <bean id="userMapper" class="com.mecewe.mapper.UserMapperImpl">-->
<!--        <property name="sqlSessionTemplate" ref="sqlSession"/>-->
<!--    </bean>-->
</beans>
```

##### **mybatis-config.xml配置**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <typeAliases>
        <package name="com.mecewe.proj"/>
    </typeAliases>
    
<!--    <settings>-->
<!--        <setting name="" value=""/>-->
<!--    </settings>-->

<!--    <mappers>-->
<!--        <mapper class="com.mecewe.mapper.UserMapper" />-->
<!--    </mappers>-->
</configuration>
```

##### **applicationContext.xml配置**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
<!--    导入配置-->
    <import resource="spring-dao.xml"/>

<!--    以下专门注册Bean-->
    <bean id="userMapper" class="com.mecewe.mapper.UserMapperImpl">
        <property name="sqlSessionTemplate" ref="sqlSession"/>
    </bean>
</beans>
```

#### 12.3 配置事例二 「简介版」

基层一个SqlSessionDaoSupport类，从而无需导入sqlSession

```java
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper {
    public List<User> selectUser() {
        return getSqlSession().getMapper(UserMapper.class).selectUser();
    }
}
```

xml中注册相应的bean

```xml
<bean id="userMapper2" class="com.mecewe.mapper.UserMapperImpl2">
  	<property name="sqlSessionFactory" ref="sqlSessionFactory"/>
</bean>
```

### 十三、声明式事务

#### 13.1 事务概念

![image-20191212221145581](/Users/mecewe/Library/Application Support/typora-user-images/image-20191212221145581.png)

#### 事务ACID原则

- 原子性（atomicity）
- 一致性（consistency）
- 隔离型（isolation）
  - 多个业务可能操作同一个资源，防止数据损坏
- 持久性（durability）
  - 事务一旦提交，无论系统发生什么问题，结果都不会再被影响，被持久化的写到存储器中

#### 13.2 spring中的事务管理

##### 声明式事务：AOP



##### 编程式事务：需要在代码中，进行事务的管理

