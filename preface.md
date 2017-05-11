# 序言

**Workerman，让你看到PHP不为人知的一面。**

## Workerman是什么？
Workerman是一款纯PHP开发的开源高性能的PHP socket 服务框架。

Workerman不是重复造轮子，它不是一个MVC框架，而是一个更底层更通用的socket服务框架，你可以用它开发tcp代理、梯子代理、游戏服务器、邮件服务器、ftp服务器、甚至开发一个php版本的redis、php版本的数据库、php版本的nginx。Workerman可以说是PHP领域的一次创新，让开发者彻底摆脱了PHP只能做WEB的束缚，向更广阔的领域前进。

实际上Workerman可以看作是一个PHP版本的nginx，核心是多进程+Epoll+非阻塞IO，每个进程能维持上万并发链接。由于Workerman本身常住内存，不依赖Apache、nginx、php-fpm这些容器，拥有超高的性能。同时支持TCP、UDP、UNIXSOCKET，支持长链接，支持Websocket、HTTP、WSS、HTTPS等通讯协以及各种自定义协议。拥有定时器、异步socket客户端、异步Mysql、异步Redis、异步Http、异步消息队列等众多高性能组件。

# Workerman的一些应用方向
Workerman不同于传统MVC框架，Workerman不仅可以用于Web开发，同时还有更广阔的应用领域，例如即时通讯类、物联网、游戏、服务治理、其它服务器或者中间件，这无疑大大提高了PHP开发者的视野。目前这些领域的PHP开发者奇缺，如果想在PHP领域有自己的技术优势，不满足于每天的增删改查工作，或者想向架构师方向或者技术大牛的方向发展，Workerman都是非值得学习的框架。建议开发者不仅会用，而且能基于Workerman开发出属于自己的开源项目，提升技能增加自己的影响力，比如[Beanbun多进程网络爬虫框架](https://github.com/kiddyuchina/Beanbun)就是一个很好的例子，刚刚上线不久就获得众多好评。

1、即时通讯
例如网页即时聊天、即时消息推送、微信小程序、手机app消息推送、PC软件消息推送等等
[[示例 workerman-chat聊天室](http://www.workerman.net/workerman-chat) 、 [web消息推送](http://www.workerman.net/web-sender) 、 [小蝌蚪聊天室](http://www.workerman.net/workerman-todpole)]

2、物联网
例如Workerman与打印机通讯、与单片机通讯、智能手环、智能家居、共享单车等等。
[客户案例如 易联云、易泊时代等]

3、游戏服务器
例如棋牌游戏、MMORPG游戏等等。[[示例 browserquest-php](http://www.workerman.net/browserquest)]

4、SOA服务化
利用Workerman将现有业务不同功能单元封装起来，以服务的形式对外提供统一的接口，达到系统松耦合、易维护、高可用、易伸缩。[[示例 workerman-json-rpc](http://www.workerman.net/workerman-jsonrpc)、 [workerman-thrift](http://www.workerman.net/workerman-thrift)]

5、开发一些其它服务器或者中间件
例如 [GatewayWorker](http://www.workerman.net/gatewaydoc/)，[PHPSocket.IO](http://www.workerman.net/phpsocket_io)，[http代理](https://github.com/walkor/php-http-proxy)，[sock5代理](https://github.com/walkor/php-socks5)，[分布式通讯组件](https://github.com/walkor/Channel)，[分布式变量共享组件](https://github.com/walkor/GlobalData)，[消息队列](https://github.com/walkor/workerman-queue)，[异步MySQL组件](http://www.kancloud.cn/walkor/workerman/315213)，[异步redis组件](http://www.kancloud.cn/walkor/workerman/315215)，[异步http组件](http://www.kancloud.cn/walkor/workerman/315217)，[异步消息队列组件](http://www.kancloud.cn/walkor/workerman/315219)，[异步dns组件](http://www.kancloud.cn/walkor/workerman/315930)，[文件监控组件](http://www.kancloud.cn/walkor/workerman/315203)，还有很多第三方开发的组件框架等等

显然传统的mvc框架很难实现以上的功能，所以这就是workerman诞生的原因。

# 理念
极简、稳定、高性能、分布式。

### **极简**
小即是美，Workerman内核极简，仅有几个php文件并且只暴露几个接口，学习起来非常简单。所有其它功能通过组件的方式扩展。

Workerman拥有完善的文档+权威的主页+活跃的社区+数个千人QQ群+众多的高性能组件+N多的例子，这一切都让开发者用来来更得心应手。

### **稳定**
Workerman已经开源数年，被很多上市公司大规模使用，超级稳定。有些服务2年多没重启过仍然在飞速运行。没有coredump、没有内存泄漏、没有bug。

### **高性能**
Workerman因为常住内存，不依赖apache/php-fpm，具有超高的性能，比起传统的MVC框架，性能要高数十倍，PHP7下通过ab压力测试QPS也略高于nginx。

### **分布式**
现在早已经不是单枪匹马的时代了，单台服务器性能再强悍也有极限，随着用户爆发式增长你发现单机无法满足需要了，这时候分布式多服务器部署才是王道。Workerman直接提供了一套长链接分布式通讯方案[GatewayWorker框架](http://www.workerman.net/gatewaydoc/)，加服务器只需要简单配置下然后启动即可，业务代码不用任何更改，系统承载能力成倍增加。如果你是开发TCP长链接应用，建议直接用[GatewayWorker](http://www.workerman.net/gatewaydoc/)，它是对Workerman的一个包装，针对长链接应用提供了更丰富的接口以及强悍的分布式处理能力。


传统的PHP应用程序基本上是在Apache等Web容器中运行的，浏览器与Web容器采用HTTP协议通信，然而在很多实际项目中HTTP协议无法满足我们的需求，尤其是在服务端和客户端要保持长连接，做实时双向通讯时，HTTP协议显得力不从心。例如即时IM通讯，游戏服务器通讯，与硬件传感器通讯等等，开发这些应用程序我们无法直接使用nginx/apache + PHP来实现，也更无法使用传统的PHP框架来做。这就迫使我们寻找一种新的解决方案，这时候WorkerMan就是你的最佳选择。

WorkerMan是一款纯PHP开发的开源的高性能的PHP socket服务器框架，基于WorkerMan开发者可以开发出各种网络服务器，例如基于websocket的服务器、游戏服务器、移动通讯服务器、智能家居服务端、物联网服务、web服务器、RPC服务器等等。几乎任何基于TCP/UDP通讯的服务端都可以用WorkerMan来开发。WorkerMan使得开发者摆脱PHP只能用于Web开发的束缚，向更广阔的前景发展。

# 本手册作用范围
WorkerMan有分为Linux版本[WorkerMan](https://github.com/walkor/workerman)和Windows版本[WorkerMan-for-win](https://github.com/walkor/workerman-for-win)，windows版本说明参见[这里](http://www.workerman.net/windows)。Linux版本可用于开发调试及正式环境部署，而由于PHP-CLI在windows系统无法实现多进程以及守护进程，所以windows版本Workerman建议仅作开发调试使用。

注意：Windows版本WorkerMan无法在Linux平台使用，同时Linux版本WorkerMan也无法在。

# windows用户（必读）

windows用户需要使用windows版本的workerman，windows版本workerman本身**不依赖任何扩展**，只需要配置好PHP环境变量即可，**windows版本workerman安装及注意事项参见[windows用户必看](http://www.workerman.net/windows)。**

# 客户端

WorkerMan的通信协议是开放的，又是可定制的，因此，理论上WorkerMan可以与使用任意协议的任意平台的客户端进行通信。当用户开发客户端时，可以根据相应的通信协议完成与服务端的通信。



