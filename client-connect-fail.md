# 客户端连接失败原因

连接失败客户端一般会有两种报错，```connection refuse``` 和 ```connection timeout```

## connection refuse（连接拒绝）
 
一般是以下原因:
1、客户端连接的端口错了
2、客户端连接的域名或者ip错了
3、如果客户端使用了域名连接，域名可能指向了错误的服务器ip
4、服务端没有启动或者端口没有被监听
5、使用了网络代理软件

## connection timeout（连接超时）
 
一般是以下原因：
1、服务器防火墙阻止了连接，可以临时关闭防火墙试下
2、如果是云服务器，安全组也可能会阻止连接建立，需要到管理后台开放对应端口
3、服务器不存在或者没有启动
4、如果客户端使用了域名连接，域名可能指向了错误的服务器ip
5、客户端访问的ip是服务器内网ip，并且客户端和服务端不在一个局域网

## 其它报错
如果发生的报错不是```connection refuse``` 和 ```connection timeout```则一般是以下原因：

1、客户端使用的通讯协议与服务端不一致。
例如服务端是http通讯协议，客户端使用websocket通讯协议访问是无法连接的。如果客户端用websocket协议连接，那么服务端必须也是websocket协议。如果服务端是http协议的服务，那么客户端必须用http协议访问。

这里的原理类似如果你要和英国人交流，那么要使用英语。如果要和日本人交流，那么要使用日语。这里的语言就类似与通许协议，双方(客户端和服务端)必须使用相同的语言才能交流，否则无法通讯。

通讯协议不一致导致的常见的报错有：

> WebSocket connection to 'ws://xxx.com:xx/' failed: Error during WebSocket handshake: Unexpected response code: xxx

> WebSocket connection to 'ws://xxx.com:xx/' failed: Error during WebSocket handshake: net::ERR_INVALID_HTTP_RESPONSE



