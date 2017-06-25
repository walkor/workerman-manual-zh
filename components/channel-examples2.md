# 例子1
**``` (要求Workerman版本>=3.3.0) ```**

基于Worker的多进程(分布式集群)分组推送系统

``` php
require_once __DIR__ . '/../Workerman/Autoloader.php';
    require_once __DIR__ . '/Channel/src/Server.php';
    require_once __DIR__ . '/Channel/src/Client.php';
    use Workerman\Worker;

    $channel_server = new Channel\Server('0.0.0.0', 2206);

    $worker = new Worker('websocket://0.0.0.0:1234');
    // 全局群组到链接的映射数组
    $group_con_map = array();
    $worker->onWorkerStart = function(){
        // Channel客户端连接到Channel服务端
        Channel\Client::connect('127.0.0.1', 2206);

        // 监听全局分组发送消息事件
        Channel\Client::on('send_to_group', function($event_data){
            $group_id = $event_data['group_id'];
            $message = $event_data['message'];
            global $group_con_map;
            var_dump(array_keys($group_con_map));
            if (isset($group_con_map[$group_id])) {
                foreach ($group_con_map[$group_id] as $con) {
                    $con->send($message);
                }
            }
        });
    };
    $worker->onMessage = function($con, $data){
        // 加入群组消息{"cmd":"add_group", "group_id":"123"}
        // 或者 群发消息{"cmd":"send_to_group", "group_id":"123", "message":"这个是消息"}
        $data = json_decode($data, true);
        var_dump($data);
        $cmd = $data['cmd'];
        $group_id = $data['group_id'];
        switch($cmd) {
            // 链接加入群组
            case "add_group":
                global $group_con_map;
                // 将链接加入到对应的群组数组里
                $group_con_map[$group_id][$con->id] = $con;
                // 记录这个链接加入了哪些群组，方便在onclose的时候清理group_con_map对应群组的数据
                $con->group_id = isset($con->group_id) ? $con->group_id : array();
                $con->group_id[$group_id] = $group_id;
                break;
            // 群发消息给群组
            case "send_to_group":
                // Channel\Client给所有服务器的所有进程广播分组发送消息事件
                Channel\Client::publish('send_to_group', array(
                    'group_id'=>$group_id,
                    'message'=>$data['message']
                ));
                break;
        }
    };
    // 这里很重要，链接关闭时把链接从全局群组数据中删除，避免内存泄漏
    $worker->onClose = function($con){
        global $group_con_map;
        // 遍历链接加入的所有群组，从group_con_map删除对应的数据
        if (isset($con->group_id)) {
            foreach ($con->group_id as $group_id) {
                unset($group_con_map[$group_id][$con->id]);
            }
            if (empty($group_con_map[$group_id])) {
                unset($group_con_map[$group_id]);
            }
        }
    };

    Worker::runAll();
```