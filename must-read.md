# workerman开发者必须知道的几个问题
**1、workerman不依赖apache或者nginx**

workerman本身已经是一个类似apache/nginx的容器，只要[PHP环境OK](http://doc.workerman.net/315116) workerman就可以运行。

**2、workerman是命令行启动的**

启动方式类似apache使用命令启动(一般网页空间无法使用workerman)。启动界面类似下面
![](image/screenshot_1495622774534.png)

**3、长链接必须加心跳**

长链接必须加心跳，长链接必须加心跳，长链接必须加心跳，重要的话说三遍。 
长链接长时间不通讯肯定会被防火墙干掉而断开。不加心跳的长链接应用就等着老板KO你吧。
[workerman心跳说明](http://doc.workerman.net/315282)、 [gatewayWorker心跳说明](http://doc2.workerman.net/326139)

**4、客户端和服务端协议一定要对应才能通讯**

这个是开发者非常常见的问题。例如客户端是用websocket协议，服务端必须也是websocket协议(服务端```new Worker('websocket://0.0.0.0...')```)才能连得上，才能通讯。 
不要在浏览器地址栏访问websocket协议端口，不要用webscoket协议访问裸tcp协议端口，协议一定要对应。

**5、链接失败可能的原因**

刚开始使用workerman时很常见的一个问题是客户端链接服务端失败。 原因一般如下： 
1、服务器防火墙(包括云服务器安全组)阻止了链接 （50%几率是这个）
2、客户端和服务端使用的协议不一致 （30%几率）
3、ip或者端口写错了 (15%的几率)
4、服务端没启动 


**6、不要使用exit die语句**

否则进程会退出，并显示WORKER EXIT UNEXPECTED错误。当然，进程退出了会立刻重启一个新的进程继续服务。

**7、改代码要重启**

workerman是常驻内存的框架，改代码要重启workerman才能看到新代码的效果。

**8、长链接应用建议用GatewayWorker框架**

很多发者使用workerman是要开发**长链接**应用，例如即时通讯、物联网等，**长链接**应用建议直接使用GatewayWorker框架，它专门在workerman的基础上再次封装，做起长链接应用后台更简单、更易用。

**9、workerman真的很牛逼**

简单、稳定、性能贼高


