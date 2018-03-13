# 微信小程序

微信小程序只能使用443端口，如果443端口被占用(表现为workerman失败)，说明这台服务器有nginx/apache占用了443端口。解决办法是用nginx/apache代理wss转发给workerman。nginx站点增加wss代理参考[workerman小程序nginx配置HTTPS WSS](http://wenda.workerman.net/?/question/1485)，apache站点增加wss代理参考这里[小程序与GatewayWorker建立连接及 apache 配置 wss 转发](http://wenda.workerman.net/?/article/24)。