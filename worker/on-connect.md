# onConnect
## 说明:
```php
callback Worker::$onConnect
```

当客户端与Workerman建立链接时(TCP三次握手完成后)触发的回调函数。每个连接只会触发一次```onConnect```回调。

## 回调函数的参数

 ``` $connection ```

连接对象，即[TcpConnection实例](http://doc.workerman.net/315157)，用于操作客户端链接，如[发送数据](http://doc.workerman.net/315165)，[关闭链接](http://doc.workerman.net/315168)等


## 范例

```php
use Workerman\Worker;
require_once __DIR__ . '/Workerman/Autoloader.php';

$worker = new Worker('websocket://0.0.0.0:8484');
$worker->onConnect = function($connection)
{
    echo "new connection from ip " . $connection->getRemoteIp() . "\n";
};
// 运行worker
Worker::runAll();
```
