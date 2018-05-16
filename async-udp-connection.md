AsyncUdpConnection可以作为一个udp客户端与远程udp服务端进行通讯。其实udp是无连接的，但是为了易用性，这里与AsyncTcpConnection命名规则和接口保持基本一致。

注意：与AsyncTcpConnection不同，AsyncUdpConnection不支持以下属性或者方法。
1. 没有connection->id属性
2. 没有connection->worker属性
3. 没有connection->transport属性
4. 没有connection->maxSendBufferSize属性
5. 没有connection->defaultMaxSendBufferSize属性
6. 没有connection->maxPackageSize属性
7. 没有connection->onBufferFull回调
8. 没有connection->onBufferDrain回调
9. 没有connection->onError回调
10. 没有connection->destroy()接口
11. 没有connection->pauseRecv()接口
12. 没有connection->resumeRecv()接口
13. 没有connection->pipe()接口
14. 没有connection->reconnect()接口

