

#SpringBoot框架

## 一、annotation介绍

#### 1、@ConfigurationProperties

> 全局自动配置

##### 1.1松散绑定(松散语法)

- @ConfigurationProperties(prefix = " ")支持该语法

![image-20191128190626026](/Users/mecewe/Library/Application Support/typora-user-images/image-20191128190626026.png)

#### 2、@PropertySource(value = "classpath:person.properties")

> 加载类路径下的某个内容

#### 3、@ImportResource(locations = {"classpath:beans.xml"})

> 导入Spring的配置文件，让配置文件里面的内容生效

#### 4、@Configuration和@Bean

>@Configuration表示这是一个配置类，可以给容器中添加组件 <=>等价于 XML中配置beans
>
>@Bean 注册bean对象. <=>等价于 XML中配置bean



#### 5、自动配置@EnableAutoConfiguration

>利用EnableAutoConfigurationImportSelector给容器中导入一些组件

#### 6、@Component

> 泛指组件，当组件不好归类时，可以使用这个注解进行标注。一般公共的方法会用上这个注解

#### 7、@Conditonal派生注解(Spring注解版原生的@Conditonal作用)

> 必须是@Conditonal指定的条件成立，才给容器中添加组件，配置类里面的所有内容才生效

![image-20191128214400652](/Users/mecewe/Library/Application Support/typora-user-images/image-20191128214400652.png)

8、@Mapper和@MapperScan(value = "com.mecewe.springboottest04mybatis.mapper")

> @Mapper用于mapper类
>
> @MapperScan省去了没个mapper类上写@Mapper的过程，批量扫描

9、@EnableAsync和@Async 开启异步注解

>@EnableAsync 开启异步注解
>
>@Async 开启异步请求

10、@EnableScheduling和@Scheduled 定时任务

>@EnableScheduling 开启定时任务
>
>@Scheduled 需要定时的任务上添加注解



## 二、相关配置信息

#### 1、profile

![image-20191128204500837](/Users/mecewe/Library/Application Support/typora-user-images/image-20191128204500837.png)

![image-20191128205119920](/Users/mecewe/Library/Application Support/typora-user-images/image-20191128205119920.png)

![image-20191128210204473](/Users/mecewe/Library/Application Support/typora-user-images/image-20191128210204473.png)

#### 2、debug=true 属性 查看自动导入配置情况 

来让控制台打印自动配置报告，来查看哪些生效，哪些未生效



## 三、日志

#### 1、日志现状

![image-20191128223018875](/Users/mecewe/Library/Application Support/typora-user-images/image-20191128223018875.png)

- JCL：最后更新2014年 旧
- jboss-logging：常用于特定框架，不常用
- JUL：与Log4j出现于同一时间，没有Log4j优秀
- Log4j2: Apach公司借了Log4j的名，很优秀，但框架适配度不高
- **SL4j、Log4j（旧，存在一定缺陷）、Logback（新，弥补缺陷）出自同一人之手**（采用）

#### 2、选用日志（SLF4j-Logback）

日志门面：SLF4j	日志实现：Logback

- spring框架默认是用JCL（Commons Logging）

- Springboot选用SLF4j和Logback

#####      2.1 如何在系统中采用SELF4J

![img](http://www.slf4j.org/images/concrete-bindings.png)

##### 	2.2 如何让系统中的日志统一到SELF4J

![image-20191129130549058](/Users/mecewe/Library/Application Support/typora-user-images/image-20191129130549058.png)

![click to enlarge](http://www.slf4j.org/images/legacy.png)

#### 3、Springboot日志系统

> Springboot能自动适配所有的日志，而底层使用SLF4j-Logback的方式记录日志，引入其他框架时，只需要把这个框架依赖的日志框架排除掉；

![image-20191129130913986](/Users/mecewe/Library/Application Support/typora-user-images/image-20191129130913986.png)

#### 4、日志的使用

> 可以调整输出日志的级别；日志就只会在这个以后的高级别生效

```java
//记录器
Logger logger = LoggerFactory.getLogger(getClass());
@Test
void testLogging(){
  //日志级别
  //由低到高 trace<debug<info<warn<error
  logger.trace("trace...");
  logger.debug("debug...");
  //Springboot默认使用info级别；root级别
  logger.info("info...");
  logger.warn("warning...");
  logger.error("error...");

}
```

可通过配置文件修改spring默认配置

```properties
logging.level.com.mecewe(包名)=trace
#两者选其一，都有的情况下加载file内容
#在当前磁盘根目录下创建log文件夹，使用spring.log作为默认文件
logging.path=/spring/log
#不指定完整路径，则在当前项目下生成Spring.log
logging.file=G:/Spring.log

#在控制台输出的的日志格式
logging.pattern.console=...
#指定文件输出的的日志格式
logging.pattern.file=...
```

![image-20191129144305098](/Users/mecewe/Library/Application Support/typora-user-images/image-20191129144305098.png)

![image-20191129140056655](/Users/mecewe/Library/Application Support/typora-user-images/image-20191129140056655.png)

#### 5、切换日志

去除之前的日志框架，改用现在的框架，如切换为log4j2(springboot有提供默认配置)：

![image-20191129145754155](/Users/mecewe/Library/Application Support/typora-user-images/image-20191129145754155.png)

## 四、web开发

#### 1、对静态资源映射的文件夹

```
classpath:/META-INF/resources/
classpath:/resources/
classpath:/static/
classpath:/public/
```

静态资源图标：

> **/favicon.ico

#### 2、模版引擎

JSP、Velocity、Freemark、Thymeleaf

#### 3、Servlet容器

tomcat(默认)、jetty(适合于长连接)、undertow(用于高并发)

![image-20191130192155796](/Users/mecewe/Library/Application Support/typora-user-images/image-20191130192155796.png)

#### 4、嵌入式Servlet容器启动原理

##### 后置处理器处理过程

![image-20191130194205266](/Users/mecewe/Library/Application Support/typora-user-images/image-20191130194205266.png)

##### 总的启动原理

![image-20191130201829466](/Users/mecewe/Library/Application Support/typora-user-images/image-20191130201829466.png)

![image-20191130201207520](/Users/mecewe/Library/Application Support/typora-user-images/image-20191130201207520.png)

IOC容器启动时创建嵌入式的Servlet容器

## 五、Springboot与Docker

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191130204821711.png" alt="image-20191130204821711" style="zoom:80%;" />

#### 1、 Docker相关命令

```shell
#docker安装
yum install docker
#启动docker
systemctl start docker
#开机启动docker
systemctl enable docker
#停止docker
systemctl stop docker

#搜索镜像
docker search mysql(关键字)
#拉取 :tag可选 默认时latest
docker pull 镜像名:tag
#列表 查看本地所有镜像
docker images
#删除指定本地某个镜像
docker rmi image-id

#运行镜像 --name 自定义容器名 -d 后台运行 image-name 后台运行模版
docker run --name container-name -d image-name
#列表 查看运行中的容器 
docker ps
# 查看所有容器
docker ps -a
#停止运行容器
docker stop container ID/container-name
#启动容器
docker start container ID/container-name
#删除容器
docker rm container ID
#启动一个端口映射的的容器 主机端口:容器端口
docker run --name container-name -d image-name -p 8888:8080 tomcat
#容器日志
docker logs container ID/container-name
  #实时查看docker容器日志
  $ sudo docker logs -f -t --tail 行数 容器名
  #例：实时查看docker容器名为s12的最后10行日志
  $ sudo docker logs -f -t --tail 10 s12
  
#查看容器的详细信息 例如mysql；
docker inspect mysql 
#docker exec 这个命令比较方便，可以在容器运行别的服务时连接上该容器；
docker exec -it ID/container-name bash
```

**需防火墙关闭**

```shell
#查看防火墙状态
service firewalld status
#关闭防火墙
service firewalld stop
```

#### ⚠️⚠️⚠️mysql数据库记得挂载

```shell
docker run --name mysql -p 3306:3306 -v /home/mysql/data:/var/lib/mysql -v /home/mysql/conf.d:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7.28
```





## 七、启动配置原理

### 0、几个重要事件回调机制

>**配置在META-INF/spring.facyories**
>
>ApplicationContextInitializer
>
>SpringApplicationRunlistener
>
>
>
>**只需放在ioc容器中**
>
>ApplicationRunner
>
>CommandLineRunner

### 1、启动流程

​	1）创建SpringApplication对象

```java
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
    this.sources = new LinkedHashSet();
    this.bannerMode = Mode.CONSOLE;
    this.logStartupInfo = true;
    this.addCommandLineProperties = true;
    this.addConversionService = true;
    this.headless = true;
    this.registerShutdownHook = true;
    this.additionalProfiles = new HashSet();
    this.isCustomEnvironment = false;
    this.lazyInitialization = false;
    this.resourceLoader = resourceLoader;
    Assert.notNull(primarySources, "PrimarySources must not be null");
    this.primarySources = new LinkedHashSet(Arrays.asList(primarySources));
  //判断当前是否是一个web应用
    this.webApplicationType = WebApplicationType.deduceFromClasspath();
  //从类路径下找到META-INF/spring.facyories配置所有ApplicationContextInitializer；然后保存起来
 this.setInitializers(this.getSpringFactoriesInstances(ApplicationContextInitializer.class));
  //从类路径下找到META-INF/spring.facyories配置所有ApplicationListener
    this.setListeners(this.getSpringFactoriesInstances(ApplicationListener.class));
  //从多个配置类中找到有main方法的主配置类
    this.mainApplicationClass = this.deduceMainApplicationClass();
  }
```

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191204202252730.png" alt="image-20191204202252730" style="zoom:50%;" />

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191204202614128.png" alt="image-20191204202614128" style="zoom:50%;" />

​	2）运行run方法

```java
public ConfigurableApplicationContext run(String... args) {
        StopWatch stopWatch = new StopWatch();
        stopWatch.start();
        ConfigurableApplicationContext context = null;
        Collection<SpringBootExceptionReporter> exceptionReporters = new ArrayList();
        this.configureHeadlessProperty();
  		//获取SpringApplicationRunListeners；从类路径下META-INF/spring.facyories
        SpringApplicationRunListeners listeners = this.getRunListeners(args);
  		//回调所有的获取SpringApplicationRunlistener.starting()方法
        listeners.starting();

        Collection exceptionReporters;
        try {
          //封装命令行参数
            ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
          //准备环境
            ConfigurableEnvironment environment = this.prepareEnvironment(listeners, applicationArguments);
          		//创建环境完成后回调SpringApplicationRunlistener.environmentPrepared()；表示环境准备完成
          
            this.configureIgnoreBeanInfo(environment);
          //打印标志
            Banner printedBanner = this.printBanner(environment);
          //创建ApplicationContext；决定创建web的ioc还是普通的ioc
            context = this.createApplicationContext();
            exceptionReporters = this.getSpringFactoriesInstances(SpringBootExceptionReporter.class, new Class[]{ConfigurableApplicationContext.class}, context);
          
          //准备上下文；将environment保存到ioc中；而且applyInitializers()
          //applyInitializers():回调之前保存的所有的ApplicationContextInitializer的initialize方法
          //回调所有的SpringApplicationRunlistener的contextPrepared()方法
            this.prepareContext(context, environment, listeners, applicationArguments, printedBanner);
          //prepareContext运行完以后回调所有的SpringApplicationRunlistener的contextLoaded()
          
//！！最重要//刷新容器；ioc容器初始化（如果是web应用还会创建嵌入式的Tomcat）
          //扫描、创建、加载所有组件的地方；（配置类、组件、自动配置）
            this.refreshContext(context);
          
          //从ioc容器中获取所有的ApplicationRunner和CommandLineRunner
          //(springboot2.x已失效)移到最后
            this.afterRefresh(context, applicationArguments);
            stopWatch.stop();
            if (this.logStartupInfo) {
                (new StartupInfoLogger(this.mainApplicationClass)).logStarted(this.getApplicationLog(), stopWatch);
            }
          
					//在所有SpringApplicationRunlistener回调started()方法(不再是finished())
            listeners.started(context);
          
          ////从ioc容器中获取所有的ApplicationRunner和CommandLineRunner
          //ApplicationRunner先回调，CommandLineRunner再回调
            this.callRunners(context, applicationArguments);
        } catch (Throwable var10) {
            this.handleRunFailure(context, var10, exceptionReporters, listeners);
            throw new IllegalStateException(var10);
        }

        try {
            listeners.running(context);
            return context;
        } catch (Throwable var9) {
            this.handleRunFailure(context, var9, exceptionReporters, (SpringApplicationRunListeners)null);
            throw new IllegalStateException(var9);
        }
    }
```



## 八、自定义starter

#### 1、需要知道的

![image-20191205004034829](/Users/mecewe/Library/Application Support/typora-user-images/image-20191205004034829.png)

![image-20191205004054239](/Users/mecewe/Library/Application Support/typora-user-images/image-20191205004054239.png)

#### 2、模式：

启动器只用作依赖导入；

专门写一个自动配置模块；

启动器依赖自动配置：别人只需引入启动器（starter）

#### 3、命名方式：

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191205004317656.png" alt="image-20191205004317656" style="zoom:50%;" />

#### 4、编写完程序，使用install安装



## 九、springboot与缓存

### 1、默认配置缓存部分*SimpleCacheConfiguration*

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191205114215363.png" alt="image-20191205114215363" style="zoom:80%;" /><img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191205114848798.png" alt="image-20191205114848798" style="zoom:50%;" />

![image-20191205125904049](/Users/mecewe/Library/Application Support/typora-user-images/image-20191205125904049.png)

#### 1、开启基于注解的缓存：@EnableCaching

#### 2、标注缓存注解即可

- @Cacheable

  >属性介绍：
  >
  >cacheNames/value:指定缓存组件的名字；
  >
  >key：缓存数据使用的key；可以用它来指定。默认是使用方法参数的值：*id-emp*
  >
  >​		编写SpEL： #id；参数id的值	#a0	#p0	#root.args[0]
  >
  >keyGenerator：key的生成器：可以自己指定key的生成器的组件id
  >
  >​		*key/keyGenerator*二选一
  >
  >cacheManager：指定缓存管理器；或者cacheResolver指定获取解析器
  >
  >condition：指定符合条件的情况下才缓存；*condition = “#id > 0”*
  >
  >unless：否定缓存；当*unless*指定条件为true，方法的返回值就不会被缓存；
  >
  >​			可以获取到结果进行判断	**unless = "#result == true"*
  >
  >sync：是否使用异步模式 为true时unless条件不支持

  <img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191205155754068.png" alt="image-20191205155754068" style="zoom:50%;" />

- @CacheEvict

- @CachePut

#### 3、原理

​	1）自动配置类：*CacheAutoConfiguration*

​	2）缓存配置类

![image-20191205200559781](/Users/mecewe/Library/Application Support/typora-user-images/image-20191205200559781.png)

​	3）哪个配置类默认生效？*SimpleCacheConfiguration*

​	4）给容器中注册了一个*CacheManager*

​	5）可以获取和创建*ConcurrentMapperCache*类型的缓存组件; 将数据保存在*ConcurrentMap*中

#### 4、运行流程

- *@Cacheable* **执行前先去检查缓存中有没有这个数据，默认按照参数的值作为key去查询缓存**

​	1）运行方法前，先去查询Cache（缓存组件），按照cachenames指定的名字获取；

​		（CacheManager现获取相应的缓存），第一次获取缓存如果没有Cache组件会自动创建。

​	2）去Cache中查找缓存的内容，使用一个key，默认就是方法的参数；

​		key是按照某种策略生成的；默认使用keyGenerator生成的，默认使用SimpleKeyGenerator

​			SimpleKeyGenerator生成key的策略：

​					如果没有参数：key = new SimpleKey()

​					如果一个参数：key = 参数的值

​					如果多个参数：key = new SimpleKey(parms)

​	3）没有查到缓存就调用目标方法；

​	4）将目标方法返回的的结果，放进缓存中

- *@CachePut*  **即调用方法，又更新缓存数据；同步更新缓存**

![image-20191205225032028](/Users/mecewe/Library/Application Support/typora-user-images/image-20191205225032028.png)

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191205225802441.png" alt="image-20191205225802441" style="zoom:45%;" />

- *@CacheEvict*

  1）属性介绍：

  >key：指定要清除的数据
  >
  >allEntries = true ：指定清除这个缓存的所有数据
  >
  >beforeInvocation = false： 缓存的清除是否在方法之前执行（false默认在方法之后）

- *@Caching* 定义复杂的缓存规则

  ![image-20191205231855717](/Users/mecewe/Library/Application Support/typora-user-images/image-20191205231855717.png)

- *@CacheConfig* 抽取缓存的公共配置

  >cacheNames = "emp"

### 2、redis部分

​	![image-20191206003946321](/Users/mecewe/Library/Application Support/typora-user-images/image-20191206003946321.png)

## 十、spring和消息-JMS&AMQP

#### 1、概念

![image-20191206235015567](/Users/mecewe/Library/Application Support/typora-user-images/image-20191206235015567.png)

#### 2、应用场景

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191206235305842.png" alt="image-20191206235305842" style="zoom:30%;" />



![image-20191206235250408](/Users/mecewe/Library/Application Support/typora-user-images/image-20191206235250408.png)

![image-20191207000946912](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207000946912.png)

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191207001400880.png" alt="image-20191207001400880" style="zoom:35%;" />

#### 3、RabbitMQ介绍

![image-20191207002337251](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207002337251.png)

![image-20191207002512050](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207002512050.png)

![image-20191207002954970](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207002954970.png)

![image-20191207003225852](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207003225852.png)

![image-20191207003347558](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207003347558.png)

#### 4、自动配置介绍

- RabbitAutoConfiguration
- 有自动配置了连接工厂
- RabbitProperties封装了RabbitMQ的配置
- RabbitTemplate：给RabbitMQ发送和接收消息
- amqpAdmin：RabbitMQ管理系统功能组件 创建和删除Queue、Exchange、Binding

- *@EnableRabbit* + *@RabbitListener*(queues = "mecewe.news") 监听消息队列的内容

#### 5、应用

> 详见代码



## 十一、spring和Elasticsearch

#### 1、Elasticsearch简介

![image-20191207213733276](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207213733276.png)

![image-20191207221121043](/Users/mecewe/Library/Application Support/typora-user-images/image-20191207221121043.png)

#### 2、java实现

![image-20191208192848156](/Users/mecewe/Library/Application Support/typora-user-images/image-20191208192848156.png)

## 十二、异步请求和定时任务、邮件任务

具体请看第一章注解

#### 2、定时任务

![image-20191208195350068](/Users/mecewe/Library/Application Support/typora-user-images/image-20191208195350068.png)

![image-20191208200222055](/Users/mecewe/Library/Application Support/typora-user-images/image-20191208200222055.png)

#### 3、邮件任务

![image-20191208200701786](/Users/mecewe/Library/Application Support/typora-user-images/image-20191208200701786.png)

## 十三、分布式

![image-20191208210159164](/Users/mecewe/Library/Application Support/typora-user-images/image-20191208210159164.png)

#### 1、Dubbo

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191208210306616.png" alt="image-20191208210306616" style="zoom:40%;" />

## 十三、springCloud

![image-20191208212820452](/Users/mecewe/Library/Application Support/typora-user-images/image-20191208212820452.png)

## 十四、监管

- 监管端点

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191208221101244.png" alt="image-20191208221101244" style="zoom:40%;" />