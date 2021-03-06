### TCP和UDP区别，UDP怎么保证传输可靠

**TCP与UDP区别总结**：

1、TCP面向连接（如打电话要先拨号建立连接）;UDP是无连接的，即发送数据之前不需要建立连接

2、TCP提供可靠的服务。也就是说，通过TCP连接传送的数据，无差错，不丢失，不重复，且按序到达;UDP尽最大努力交付，即不保证可靠交付
3、TCP面向字节流，实际上是TCP把数据看成一连串无结构的字节流;UDP是面向报文的
UDP没有拥塞控制，因此网络出现拥塞不会使源主机的发送速率降低（对实时应用很有用，如IP电话，实时视频会议等）
4、每一条TCP连接只能是点到点的;UDP支持一对一，一对多，多对一和多对多的交互通信
5、TCP首部开销20字节;UDP的首部开销小，只有8个字节
6、TCP的逻辑通信信道是全双工的可靠信道，UDP则是不可靠信道

**UDP如何实现可靠传输**

由于在传输层UDP已经是不可靠的连接，那就要在应用层自己实现一些保障可靠传输的机制

简单来讲，要使用UDP来构建可靠的面向连接的数据传输，就要实现类似于TCP协议的

- 超时重传（定时器）
- 有序接受 （添加包序号）
- 应答确认 （Seq/Ack应答机制）
- 滑动窗口流量控制等机制 （滑动窗口协议）

等于说要在传输层的上一层（或者直接在应用层）实现TCP协议的可靠数据传输机制，比如使用UDP数据包+序列号，UDP数据包+时间戳等方法。

目前已经有一些实现UDP可靠传输的机制，比如

**UDT（UDP-based Data Transfer Protocol）**

基于UDP的数据传输协议（UDP-based Data Transfer Protocol，简称UDT）是一种互联网数据传输协议。UDT的主要目的是支持高速广域网上的海量数据传输，而互联网上的标准数据传输协议TCP在高带宽长距离网络上性能很差。 顾名思义，UDT建于UDP之上，并**引入新的拥塞控制和数据可靠性控制机制**。UDT是**面向连接的双向的应用层协议**。它同时**支持可靠的数据流传输和部分可靠的数据报传输**。 由于UDT完全在UDP上实现，它也可以应用在除了高速数据传输之外的其它应用领域，例如点到点技术（P2P），防火墙穿透，多媒体数据传输等等。
