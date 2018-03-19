## linux系统下workerman如何开机自动启动

打开/etc/rc.local，在exit 0前添加类似以下代码

```
/usr/bin/env php /磁盘/路径/start.php start -d

exit 0
```