# send 方法
```php
void AsyncUdpConnection::send(string $data)
```
执行异步连接操作。此方法会立刻返回。

### 参数
 ``` $data ```
向服务端发送的数据，数据大小不能超过65507字节，否则会发送失败。

### 返回值
无返回值

### 示例 

```php
use Workerman\Worker;
use Workerman\Connection\AsyncUdpConnection;
use Workerman\Lib\Timer;

$worker = new Worker('udp://0.0.0.0:1234');
$worker->onWorkerStart = function(){
    // 1秒后启动一个udp客户端，连接1234端口并发送字符串 hi
    Timer::add(1, function(){
        $udp_connection = new AsyncUdpConnection('udp://127.0.0.1:1234');
        $udp_connection->onConnect = function($udp_connection){
            $udp_connection->send('hi');
        };
        $udp_connection->onMessage = function($udp_connection, $data){
            // 收到服务端返回的数据 hello
            echo "recv $data\r\n";
        };
        $udp_connection->connect();
    }, null, false);
};
$worker->onMessage = function($connection, $data)
{
    // 收到AsyncUdpConnection客户端发来的数据，返回字符串 hello
    $connection->send("hello");
};
Worker::runAll();             
```

执行后打印类似:
```
recv hello
```

