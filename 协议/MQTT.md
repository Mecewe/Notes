https://www.cnblogs.com/shanyou/p/4085802.html

![image-20191114110215260](/Users/mecewe/Library/Application Support/typora-user-images/image-20191114110215260.png)



两者的应用场景不一样：
两者之所有有交集，是因为一个应用场景：如何通过HTML5应用来作为MQTT的客户端，以便接受设备消息或者向设备发送信息，那么MQTT over WebSocket自然成了最合理的途径了。MQTT是为了物联网场景设计的基于TCP的Pub/Sub协议，有许多为物联网优化的特性，比如适应不同网络的QoS、层级主题、遗言等等。
WebSocket是为了HTML5应用方便与服务器双向通讯而设计的协议，HTTP握手然后转TCP协议，用于取代之前的Server Push、Comet、长轮询等老旧实现。

mqtt over websocket的思路，是想既利用mqtt的诸多优良特点，同时又可以对防火墙友好，不需要找IT开1883/8883端口。