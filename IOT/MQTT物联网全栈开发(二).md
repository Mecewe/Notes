##MQTT物联网全栈开发(二)

### 后端

通过长连接的方式连接阿里云物联网平台，同时连接Apollo，实现在接收到阿里云物联网平台的数据后，实时的`publish`到Apollo消息代理中间件上。

通过阿里云物联网平台的在线调试模拟设备，发送给我们服务器模拟数据。

![image-20191121222036360](/Users/mecewe/Library/Application Support/typora-user-images/image-20191121222036360.png)

最后我们登陆http://\*.\*.\*.\*:61680，可以看到有一个长连接(来自java程序)以及收到的数据。

![image-20191121221250409](/Users/mecewe/Library/Application Support/typora-user-images/image-20191121221250409.png)

### 前端

因为Apollo就是一个消息代理工具，我们可以直接前端通过websocket连接订阅得到想要的数据。

> WebSocket 是一种在单个 TCP 连接上进行全双工通讯的协议。WebSocket 通信协议于2011年被 IETF 定为标准 RFC 6455，并由 RFC 7936 补充规范。WebSocket API 也被 W3C 定为标准。
>
> WebSocket 使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。 —— 摘自 维基百科 WebSocket

这里采用MQTT.js作为连接工具。

> MQTT.js 一个 MQTT 协议的客户端库，用 JavaScript 编写，可用于 Node.js 和浏览器。在 Node.js 端可以通过全局安装使用命令行连接，同时还支持 MQTT ，MQTT TLS 证书连接；值得一提的是 MQTT.js 还对微信小程序有较好的支持。

MQTT.js 包可以通过 [http://unpkg.com](http://unpkg.com/) 获得

```javascript
<script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>
```

####建立websocket连接

```javascript
// 连接选项
const options = {
  connectTimeout: 4000, // 超时时间
  // 认证信息
  clientId: 'emqx-connect-via-websocket',//连接Apollo时无特定要求
  username: 'emqx-connect-via-websocket',//admin
  password: 'emqx-connect-via-websocket',//password
}

const client = mqtt.connect('ws://*.*.*.*:61623', options)//你的服务器ip
```

⚠️需要注意的是：对于ws(非加密)、wss(SSL 加密) 等的连接Apollo的端口存在区别。

![image-20191121224337160](/Users/mecewe/Library/Application Support/typora-user-images/image-20191121224337160.png)

#### 订阅/取消服务

需要订阅特定的topic，才能得到相应的数据。

``````javascript
//订阅主题
client.subscribe(topic,{ qos: 1 },err =>{
  if(!err){
    	console.log("订阅成功")
    	//方法
  }else{
    	console.log("订阅失败")
  }
})

// 取消订阅
client.unubscribe(
  // topic, topic Array, topic Array-Onject
  'hello',err=>{
    if(!err){
    	console.log("取消成功")
    	//方法
    }else{
        console.log("取消失败")
    }
  }
)
``````

#### 发布/接收数据

``````javascript
//发布数据
client.publish('hello', 'hello EMQ', (error) => {
  console.log(error || '消息发布成功')
})
// 监听接收消息事件
client.on('message', (topic, message) => {
  console.log('收到来自', topic, '的消息', message.toString())
})
``````

参考资料：https://www.eotodo.com/stydy/zero/xue31.html

MQTT.js技术文档：https://www.npmjs.com/package/mqtt



#### 完结

> 通过MQTT实现物联网数据的实时传输。