# Netty的LengthFieldBasedFrameDecoder的用法详解

### 前言

**LengthFieldBasedFrameDecoder**类是Netty提供的用来解析带长度字段数据包的类，继承自**ByteToMessageDecoder**类。

### 一，粘包与拆包问题

经典的粘包拆包问题在Netty的官网文档中已经有很详细的解释，这里我直接复制过来：

>In a stream-based transport such as TCP/IP, received data is stored into a socket receive buffer. Unfortunately, the buffer of a stream-based transport is not a queue of packets but a queue of bytes. It means, even if you sent two messages as two independent packets, an operating system will not treat them as two messages but as just a bunch of bytes. Therefore, there is no guarantee that what you read is exactly what your remote peer wrote. For example, let us assume that the TCP/IP stack of an operating system has received three packets:
>
>+—–+—–+—–+
>| ABC | DEF | GHI |
>+—–+—–+—–+
>
>Because of this general property of a stream-based protocol, there’s high chance of reading them in the following fragmented form in your application:
>
>+—-+——-+—+—+
>| AB | CDEFG | H | I |
>+—-+——-+—+—+
>
>Therefore, a receiving part, regardless it is server-side or client-side, should defrag the received data into one or more meaningful frames that could be easily understood by the application logic. In case of the example above, the received data should be framed like the following:
>
>+—–+—–+—–+
>| ABC | DEF | GHI |
>+—–+—–+—–+

大意是，TCP发送的数据顺序是符合不会变但是会有拆分和合并，对端接收到的数据包不是发送方的分包格式，所以一般的做法是在包头固定字节出加入length字段，指明包长度，有接受方根据包长度拼接或者剪裁收到的数据形成完整的数据包。

### 二，LengthFieldBasedFrameDecoder的用法

我们用一个典型的包结构来举例
|+0xF7F7+|+0x000D+|+“12345678”+|
其中0xF7F7是先导码，用来标记包的开头，0x000D是长度字段，在这里要注意，长度字段可能有两种情况，一种是长度字段是整个包的长度，这里的0x000D就是这种，另一种是长度字段值是从长度字段位置起（不包含长度字段本身），到包末尾的长度。Netty默认是第二种情况。

LengthFieldBasedFrameDecoder就是Netty自带的，用来根据长度字段解析数据包的类，LengthFieldBasedFrameDecoder的完整构造参数如下：

```java
public LengthFieldBasedFrameDecoder(
ByteOrder byteOrder,
int lengthFieldOffset,
int lengthFieldLength,
int lengthAdjustment,
int initialBytesToStrip,
boolean failFast)
```

`byteOrder`是指明Length字段是大端序还是小端序，因为Netty要读取Length字段的值，所以大端小端要设置好，默认Netty是大端序ByteOrder.BIG_ENDIAN。

`maxFrameLength`是指最大包长度，如果Netty最终生成的数据包超过这个长度，Netty就会报错。

`lengthFieldOffset`是指明Length的偏移位，在这里应该是2，因为先导码有2个Byte。

`lengthFieldLength`是Length字段长度，这里是2，Length字段占2个Byte。

`lengthAdjustment` 这个参数很多时候设为负数，这是最让小伙伴们迷惑的。下面我用一整段话来解释这个参数：
当Netty利用lengthFieldOffset（偏移位）和lengthFieldLength（Length字段长度）成功读出Length字段的值后，Netty认为这个值是指从Length字段之后，到包结束一共还有多少字节，如果这个值是13，那么Netty就会再等待13个Byte的数据到达后，拼接成一个完整的包。但是更多时候，Length字段的长度，是指整个包的长度，如果是这种情况，当Netty读出Length字段的时候，它已经读取了包的4个Byte的数据，所以，后续未到达的数据只有9个Byte，即13 - 4 = 9，这个时候，就要用lengthAdjustment来告诉Netty，后续的数据并没有13个Byte，要减掉4个Byte，所以lengthAdjustment要设为 -4！！！

`initialBytesToStrip`之前的几个参数，已经足够netty识别出整个数据包了，但是很多时候，调用者只关心包的内容，包的头部完全可以丢弃掉，initialBytesToStrip就是用来告诉Netty，识别出整个数据包之后，我只要从initialBytesToStrip起的数据，比如这里initialBytesToStrip设置为4，那么Netty就会跳过包头，解析出包的内容“12345678”。

`failFast` 参数一般设置为true，当这个参数为true时，netty一旦读到Length字段，并判断Length超过maxFrameLength，就立即抛出异常。
