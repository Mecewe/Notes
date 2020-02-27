## MQTT物联网全栈开发(一)

### 硬件端

设备数据上云，连接阿里物联网云平台（通过三元组信息绑定）。略

### 软件端

#### 方法一（最简单高效的）

可以通过[阿里云IoTStudio](https://studio.iot.aliyun.com/)进行直接的拖拽式开发，同时不需要考虑接口等问题，能够直接映射云平台上某个设备对应的数据。

> 相应的缺点是不适合成熟项目的开发

####方法二

阿里云平台通过HTTP/2通道进行消息流转。配置HTTP/2服务端订阅后，物联网平台会将产品下所有设备的已订阅类型消息，通过HTTP/2通道推送至服务端。

![img](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18849/156291484112665_zh-CN.png)

之后再通过websocket与自己搭建的前端应用通信，实现实时传输。

这是服务端订阅Demo：[HTTP/2 SDK (Java) server side demo](http://aliyun-iot.oss-cn-hangzhou.aliyuncs.com/java-http2-sdk-demo/http2-server-side-demo.zip?spm=a2c4g.11186623.2.13.2c616c873ThBM0&file=http2-server-side-demo.zip)

#####Apollo的搭建

同时需要将从阿里物联网平台接收的数据以`websocket`的形式传输，所以这里使用mqtt服务的中间件——Apollo。

>Apollo以ActiveMQ原型为基础，是一个更快、更可靠、更易于维护的消息代理工具。Apache称Apollo为最快、最强健的STOMP（Streaming Text Orientated Message Protocol，流文本定向消息协议）服务器. 它采用一个完全不同的消息分发架构，同ActiveMQ一样支持多种协议。如STOMP,AMQP,MQTT,Openwire,SSL和WebSockets.

######**具体的搭建步骤**：

**一：linux下Apollo的安装**

下载`apache-apollo-1.7-unix-distro.tar.gz`文件放到`/opt`目录下面

``````shell
#加压缩文件 
tar -zxvf apache-apollo-1.7-unix-distro.tar.gz
``````

**二：创建`broker`实例**

一个broker实例是一个文件夹，其中包含所有的配置文件及运行时的数据，比如日志和消息数据。Apollo强烈建议不要把实例同安装文件放在一起。

在linux操作系统下面，建议将实例建在`/opt/lib/`目录下面

``````shell
cd /opt/lib
/opt/apache-apollo-1.7/bin/apollo create mybroker
``````

创建成功后，在`/var/lib/mybroker`目录下可以看到如下目录

bin———————实例的启动脚本
etc——————–实例的配置文件
data——————消息持久化数据
log———————运行日志
tmp——————-临时文件

**三：Apollo监控页面配置**

`vi /opt/lib/mybroker/etc/apollo.xml`

将修改
`http://127.0.0.1:61680“/>`
`https://127.0.0.1:61681“/>`
为
`http://0.0.0.0:61680“/>`
`https://0.0.0.0:61681“/>`

**四：后台启动服务**

```shell
#开启apollo
./bin/apollo-broker-service start

#关闭apollo
.bin/apollo-broker-service stop 

#重启apollo
.bin/apollo-broker-service restart
```

**六：访问Apollo的监控页面http://localhost:61680/ **

默认用户名、密码为：admin/password



——>**MQTT物联网全栈开发(二)**

> java代码实现以及前端websocket连接