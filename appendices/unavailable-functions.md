# 不支持的函数

不支持的函数/语句  | 替代方案 | 说明
----|------|----
php://input | $GLOBALS['HTTP_RAW_POST_DATA'] | 用于HTTP协议下的应用获取POST的原始数据
exit | return | 使用exit会导致进程退出，如果要返回请直接用return语句
die | return | 使用die会导致进程退出，如果要返回请直接用return语句
header | Workerman\Protocols\Http::header  | header函数只能用于http协议，其他协议不支持header

