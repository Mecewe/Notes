# spring-boot:spring-boot2.0配置druid连接池

### 文章目录

​	关于druid
​	如何配置
​		添加maven依赖
​		编辑配置文件
​		测试
​	项目地址
​	参考文章

### 关于druid

> druid自称是Java语言中最好的数据库连接池，其本身作为阿里团队的御用连接池，也证明了其性能上的实力。
> 配置方面，从sping-boot2.0开始，可以使用一个配置文件直接搞定，**不用再定义Config类**，使代码更加简洁，这点是我最满意的。
>
> 监控方面，druid自带UI监控页面，可以使用自定义访问地址和账号密码，使SQL监控更加容易。不过很恶心的是，不知什么时候开始，监控页面底部开始有阿里云的广告了，这点做得太让人恶心了。



### 如何配置

#### 添加maven依赖

##### druid依赖

```xml
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>druid-spring-boot-starter</artifactId>
   <version>1.1.10</version>
</dependency>
```

##### jdbc依赖

java连接数据库都是通过jdbc，druid只是连接池，当然也不例外。
不过我一般使用mybatis，mybatis的依赖中包含jdbc依赖。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

或者

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.2</version>
</dependency>
```
##### mysql依赖

这里就取决于个人使用的数据库了，我一般使用mysql。

```xml
<dependency>
		<groupId>mysql</groupId>
		<artifactId>mysql-connector-java</artifactId>
</dependency>
```

此处不用指定版本号，使用parent依赖里的版本即可。

### 编辑配置文件

使用IDE，还会有代码提示功能。

```properties
#JDBC基本配置

spring.datasource.druid.url=
spring.datasource.druid.username=
spring.datasource.druid.password=

#如果不是mysql，换成对应的driver-class-name即可
spring.datasource.druid.driver-class-name=com.mysql.cj.jdbc.Driver

#连接池配置
spring.datasource.druid.initial-size=5
spring.datasource.druid.max-active=100
spring.datasource.druid.min-idle=5
spring.datasource.druid.max-wait=60000
spring.datasource.druid.pool-prepared-statements=true
spring.datasource.druid.max-pool-prepared-statement-per-connection-size=20
spring.datasource.druid.validation-query=SELECT 1 FROM DUAL
spring.datasource.druid.validation-query-timeout=60000
spring.datasource.druid.test-on-borrow=false
spring.datasource.druid.test-on-return=false
spring.datasource.druid.test-while-idle=true
spring.datasource.druid.time-between-eviction-runs-millis=60000
spring.datasource.druid.min-evictable-idle-time-millis=100000

###监控配置 begin###

# WebStatFilter配置，说明请参考Druid Wiki，配置_配置WebStatFilter
spring.datasource.druid.web-stat-filter.enabled=true
spring.datasource.druid.web-stat-filter.url-pattern=/*
spring.datasource.druid.web-stat-filter.exclusions=*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*

# StatViewServlet配置，说明请参考Druid Wiki，配置_StatViewServlet配置
spring.datasource.druid.stat-view-servlet.enabled= true
spring.datasource.druid.stat-view-servlet.url-pattern= /druid/*
spring.datasource.druid.stat-view-servlet.reset-enable= false
spring.datasource.druid.stat-view-servlet.login-username= admin
spring.datasource.druid.stat-view-servlet.login-password= admin
spring.datasource.druid.stat-view-servlet.allow= 127.0.0.1

###监控配置 end###

# 配置StatFilter
spring.datasource.druid.filter.stat.db-type=mysql
spring.datasource.druid.filter.stat.log-slow-sql=true
spring.datasource.druid.filter.stat.slow-sql-millis=5000

# 配置WallFilter
spring.datasource.druid.filter.wall.enabled=true
spring.datasource.druid.filter.wall.db-type=mysql
spring.datasource.druid.filter.wall.config.delete-allow=false
spring.datasource.druid.filter.wall.config.drop-table-allow=false
```

### 测试

本地访问http://127.0.0.1:8080/druid，输入配置文件中的账号密码，即可。

![blog](https://img-blog.csdnimg.cn/20181218000035383)