# 停止失败

## 现象：
运行 ```php start.php stop``` 提示 ```stop fail```

## 原因：几种可能性

**第一种可能性：**<br>
前提是以debug方式启动的workerman，开发者在终端按了```ctrl z```给workerman发送了```SIGSTOP```信号，导致workerman进入后台并挂起(暂停)，所以无法响应stop命令(```SIGINT```信号)。

**解决：**<br>
在启动workerman的终端输入```fg```(发送```SIGCONT```信号)然后回车，将workerman切回前台运行，按```ctrl c```(发送```SIGINT```信号)停止workerman。

如果无法停止，尝试运行以下两条命令
```
killall -9 php
```
```
ps aux|grep WorkerMan|awk '{print $2}'|xargs kill -9
```
<br>
**第二种可能性：**<br>
运行stop的用户和workerman启动用户不一致，即stop用户没有权限停止workerman。

**解决：**
切换到启动workerman的用户，或者用权限更高的用户停止workerman。

<br>
**第三种可能性：**<br>
保存workerman主进程pid文件被删除，导致脚本找不到pid进程，导致停止失败。

**解决：**
将pid文件保存到安全的位置，参见手册[Worker::$pidFile](http://doc.workerman.net/315139)。


