# RabbitMQ常用命令

```bash
# 开启rabbitmq
systemctl start rabbitmq-server
# 查看状态
systemctl status rabbitmq-server
# 关闭
systemctl stop rabbitmq-server

# 开启web管理插件
rabbitmq-plugins enable rabbitmq_management

# 查看所有用户
rabbitmqctl list_users
# 创建账号
rabbitmqctl add_user 用户名 密码
# 设置用户角色为管理员
rabbitmqctl set_user_tags 用户名 administrator
# 设置用户权限（所有资源的读写权限）
rabbitmqctl set_permissions -p "/" 用户名 ".*" ".*" ".*"

# 下载延迟队列插件
# 1.先在官网下载好并上传到服务器(地址：https://github.com/rabbitmq/rabbitmq-delayed-message-exchange/releases)
rabbitmq_delayed_message_exchange-3.10.2.ez
# 2.进入该文件目录下给rabbitmq添加插件
docker cp rabbitmq_delayed_message_exchange-3.10.2.ez rabbitmq:/plugins
# 3.进入rabbitmq容器内容
docker exec -it rabbitmq bash
# 4.开启rabbitmq的延迟队列插件
rabbitmq-plugins enable rabbitmq_delayed_message_exchange
# 5.重启rabbitmq
docker restart rabbitmq
# 6.检查：在exchanges中Type下拉框中出现x-delayed-message即成功
```

