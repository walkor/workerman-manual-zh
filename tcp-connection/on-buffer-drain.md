# onBufferDrain
## 说明:
```php
callback Connection::$onBufferDrain
```

作用与[Worker::$onBufferDrain](http://doc.workerman.net/315151)回调相同，区别是只针对当前连接起作用，即可以单独设置某个连接的onBufferDrain回调
