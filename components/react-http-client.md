# react/http-client
**``` (要求Workerman版本>=3.3.6) ```**

## 安装：
```
composer require react/http-client
```

## 示例：

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';
use Workerman\Worker;

$worker = new Worker('tcp://0.0.0.0:6161');

$worker->onMessage = function($connection, $host) {
    $loop    = Worker::getEventLoop();
    $client  = new \React\HttpClient\Client($loop);
    $request = $client->request('GET', trim($host));
    $request->on('error', function(Exception $e) use ($connection) {
        $connection->send($e);
    });
    $request->on('response', function ($response) use ($connection) {
        $response->on('data', function ($data) use ($connection) {
            $connection->send($data);
        });
    });
    $request->end();
};

Worker::runAll();
```

## 文档：
https://github.com/reactphp/http-client

## 注意：
1、所有的异步编码必须在```onXXX```回调中编写

2、异步客户端需要的```$loop```变量请使用```Worker::getEventLoop();```返回值



