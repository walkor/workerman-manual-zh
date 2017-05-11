# 序言

**Workerman，让你看到PHP的真正强大之处。**

## Workerman是什么？
Workerman是一款纯PHP开发的开源高性能的PHP socket 服务器框架。被广泛的用于手机app、移动通讯，微信小程序，手游服务端、网络游戏、PHP聊天室、硬件通讯、智能家居、车联网、物联网等领域的开发。 支持TCP长连接，支持Websocket、HTTP等协议，支持自定义协议。

# Workerman应用的几个方向

1、即时通讯
例如网页即时聊天、即时消息推送、手机app消息推送、PC软件消息推送等等

2、物联网
例如Workerman与打印机通讯、与单片机通讯、智能手环、智能家居等等

3、游戏服务器
例如棋牌游戏、

4、SOA服务化
将业务解耦，分成不同的服务，

workerman可以看作是一个PHP版本的nginx，核心是Epoll+非阻塞IO，能维持上万并发链接，并提供异步socket客户端、定时器等接口，自带一个WebServer。

内核极简，通过组件扩充功能。拥有异步Mysql、异步Redis、异步Http、异步消息队列等众多高性能组件。

秉承极简、稳定、高性能的开发理念。

什么时候该用Workerman？

## 传统PHP架构
传统PHP架构一般是用Apache+mod_php或者nginx+php-fpm.
## 传统PHP架构的缺点(以nginx+php-fpm为例)
1、性能比较差
php-fpm初始化一切又销毁一切的开销。
nginx的本身开销
nginx到phpfpm的通讯开销
2、无法应对http以外的协议
websocket 

3、无法常住内存

4、无法与客户端保持长链接

传统的PHP应用程序基本上是在Apache等Web容器中运行的，浏览器与Web容器采用HTTP协议通信，然而在很多实际项目中HTTP协议无法满足我们的需求，尤其是在服务端和客户端要保持长连接，做实时双向通讯时，HTTP协议显得力不从心。例如即时IM通讯，游戏服务器通讯，与硬件传感器通讯等等，开发这些应用程序我们无法直接使用nginx/apache + PHP来实现，也更无法使用传统的PHP框架来做。这就迫使我们寻找一种新的解决方案，这时候WorkerMan就是你的最佳选择。

WorkerMan是一款纯PHP开发的开源的高性能的PHP socket服务器框架，基于WorkerMan开发者可以开发出各种网络服务器，例如基于websocket的服务器、游戏服务器、移动通讯服务器、智能家居服务端、物联网服务、web服务器、RPC服务器等等。几乎任何基于TCP/UDP通讯的服务端都可以用WorkerMan来开发。WorkerMan使得开发者摆脱PHP只能用于Web开发的束缚，向更广阔的前景发展。

# 本手册作用范围
WorkerMan有分为Linux版本[WorkerMan](https://github.com/walkor/workerman)和Windows版本[WorkerMan-for-win](https://github.com/walkor/workerman-for-win)，windows版本说明参见[这里](http://www.workerman.net/windows)。Linux版本可用于开发调试及正式环境部署，而由于PHP-CLI在windows系统无法实现多进程以及守护进程，所以windows版本Workerman建议仅作开发调试使用。

注意：Windows版本WorkerMan无法在Linux平台使用，同时Linux版本WorkerMan也无法在。

# windows用户（必读）

windows用户需要使用windows版本的workerman，windows版本workerman本身**不依赖任何扩展**，只需要配置好PHP环境变量即可，**windows版本workerman安装及注意事项参见[windows用户必看](http://www.workerman.net/windows)。**

# 客户端

WorkerMan的通信协议是开放的，又是可定制的，因此，理论上WorkerMan可以与使用任意协议的任意平台的客户端进行通信。当用户开发客户端时，可以根据相应的通信协议完成与服务端的通信。



