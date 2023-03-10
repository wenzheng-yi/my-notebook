TCP是怎样建立/断开连接的？

HTTP是基于TCP实现的，TCP建立连接是“三次握手”，断开连接是”四次挥手“。

第一次握手成功让服务端知道了客户端具有发送能力，第二次握手成功让客户端知道了服务端具有接收和发送能力，但此时服务端并不知道客户端是否接收到了自己发送的消息，所以第三次握手就起到了这个作用。经过三次通信后，服务端和客户端都确认了双方的接收和发送能力。

为什么建立连接只通信了三次，而断开连接却用了四次？

因为当服务端收到客户端的 FIN 报文后，发送的 ACK 报文只是用来应答的，并不表示服务端也希望立即关闭连接。

当只有服务端把所有的报文都发送完了，才会发送 FIN 报文，告诉客户端可以断开连接了，因此在断开连接时需要四次挥手。

| 协议版本 | 解决的核心问题           | 解决方式                               |
| -------- | ------------------------ | -------------------------------------- |
| 0.9      | HTML 文件传输            | 确立了客户端请求、服务端响应的通信流程 |
| 1.0      | 不同类型文件传输         | 设立头部字段                           |
| 1.1      | 创建/断开 TCP 连接开销大 | 建立长连接进行复用                     |
| 2        | 并发数有限               | 二进制分帧                             |
| 3        | TCP 丢包阻塞             | 采用 UDP 协议                          |



HTTP(Hyper Text Transfer Protocol)，超文本传输协议。

TCP/IP 协议族按层次分，分为4层：应用层、传输层、网络层和数据链路层。