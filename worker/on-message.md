# onMessage
## 说明:
```php
callback Worker::$onMessage
```

当客户端通过链接发来数据时触发的回调函数

## 回调函数的参数

 ``` $connection ```

连接对象，即[TcpConnection实例](http://doc.workerman.net/315157)，用于操作客户端链接，如[发送数据](http://doc.workerman.net/315165)，[关闭链接](http://doc.workerman.net/315168)等

 ``` $data ```

客户端连接上发来的数据，如果Worker指定了协议，则$data是对应协议decode（解码）了的数据


## 范例

```php
use Workerman\Worker;
require_once __DIR__ . '/Workerman/Autoloader.php';

$worker = new Worker('websocket://0.0.0.0:8484');
$worker->onMessage = function($connection, $data)
{
    var_dump($data);
    $connection->send('receive success');
};
// 运行worker
Worker::runAll();
```
