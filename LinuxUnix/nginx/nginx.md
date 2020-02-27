

## Nginx

### 一、基本概念

#### 1.1 用途

- 反向代理
- 负载均衡
- 动静分离
- 高可用

#### 1.2、反向代理

#### （1） 正向代理

![image-20200114140233254](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114140233254.png)

#### （2）反向代理

![image-20200114140121938](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114140121938.png)

![image-20200114140312262](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114140312262.png)

#### 1.3 负载均衡

 ![image-20200114141037738](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114141037738.png)

![image-20200114141406186](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114141406186.png)

#### 1.4 动静分离

![image-20200114141508556](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114141508556.png)

就是**前后端分离**

![image-20200114141842997](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114141842997.png)

### 二、Nginx安装

#### 2.1 nginx操作命令

必须进入nginx目录

/user/local/nginx/sbin

```shell
#查看版本号
./nginx -v

#启动nginx
./nginx

#关闭nginx
./nginx -s stop

#重新加载
./nginx -s reload

```

#### 2.2 nginx配置文件

#### （1）位置

> /user/local/nginx/confg/nginx.conf
>
> 或 
>
> /etc/nginx/nginx.conf

#### （2）配置组成 



有三部分组成

##### 1.全局块

![image-20200114183006873](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114183006873.png)

##### 2.events块

（该配置对nginx的性能影响较大，应灵活配置）

![image-20200114183125660](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114183125660.png)

##### 3. http块（包括**http全局块**、**server块**(全局server块、location块)）

配置最频繁对部分，代理、缓存和日志定义等绝大多数功能和第三方模块等配置都在这里	。

- **http全局块**
  - http全局配置的的指令包括文件引入、MIME-TYPE引入、日志定义、连接超时时间、单链接请求数上线等
- **server块**
  - 和虚拟机有密切关系，虚拟主机从用户看，和一台独立的硬件主机完全一样，该技术的产生是为了节省互联网服务器的硬件成本。
  - 每个http块可以包括多个server块，而每个server块相当于一个虚拟主机



​	每个**server块**也分为**全局server块**，和可以多个**location块**

- 全局server块：

![image-20200114184404958](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114184404958.png)

- location块

![image-20200114184440315](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114184440315.png)

⚠️Tip：修改windows的Host文件中域名与ip的对应关系

![image-20200114190001857](/Users/mecewe/Library/Application Support/typora-user-images/image-20200114190001857.png)



### 三、 nginx配置实例

#### 3.1 反向代理

#### （一）实例一

![image-20200124004454243](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124004454243.png)

#### （二）实例二

- 目的

![image-20200124005418486](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124005418486.png)

- 配置 （～正则表达式）

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20200124005319259.png" alt="image-20200124005319259" style="zoom:53%;" />

- 再重新加载配置命令

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20200124005824947.png" alt="image-20200124005824947" style="zoom:50%;" />

#### （三）location指令说明

该指令用于匹配URL

语法如下

```shell
location [ = | ~ | ~* | ^~] url {
	
}
```

![image-20200124010605923](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124010605923.png)

#### 3.2 负载均衡

#### （一）配置

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20200124011239470.png" alt="image-20200124011239470" style="zoom:40%;" />

#### （二）策略（请求分配方式）

##### 	1. 轮询

![image-20200124011927451](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124011927451.png)

##### 	2. weight

![image-20200124012024487](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124012024487.png)

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20200124012214660.png" alt="image-20200124012214660" style="zoom:50%;" />

##### 	3. ip_hash （解决session共享问题）

![image-20200124012249519](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124012249519.png)

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20200124012303918.png" alt="image-20200124012303918" style="zoom:50%;" />

##### 	4. fair (第三方)

![image-20200124012540224](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124012540224.png)

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20200124012551047.png" alt="image-20200124012551047" style="zoom:50%;" />

![image-20200124012710096](/Users/mecewe/Library/Application Support/typora-user-images/image-20200124012710096.png)

