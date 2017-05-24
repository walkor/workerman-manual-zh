# workerman开发者必须知道的几个问题
**1、workerman不依赖apache或者nginx**

workerman本身已经是一个类似apache/nginx的socket服务器框架，只要[PHP环境OK](http://doc.workerman.net/315116)就可以运行。

**2、workerman是命令行启动的**

启动方式类似apache使用命令启动(一般网页空间无法使用workerman)。启动类似下面
![](image/screenshot_1495620510498.png)

**3、长链接必须加心跳**

长链接必须加心跳，长链接必须加心跳，长链接必须加心跳，重要的话说三遍。 
长链接长时间不通讯肯定会被防火墙干掉而断开。不加心跳的长链接应用就等着老板KO你吧。
[workerman心跳说明](http://doc.workerman.net/315282)、 [gatewayWorker心跳说明](http://doc2.workerman.net/326139)

**4、客户端和服务端协议一定要对应才能通讯**

例如客户端是用websocket协议来通讯，服务端必须也是websocket协议(服务端```new Worker('websocket://0.0.0.0...')```)，否则肯定通讯不了。 
不要在浏览器地址栏访问websocket协议端口，不要用webscoket协议访问裸tcp协议端口。

**5、不要使用exit die语句**

否则进程会退出，并显示WORKER EXIT UNEXPECTED错误。

**6、改代码要重启**

workerman是常驻内存的框架，改代码要重启workerman才能看到新代码的效果。


