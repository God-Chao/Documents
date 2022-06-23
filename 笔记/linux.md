# Linux

## 1.文件管理

```bash
# 查看该目录下的所有资源
ls
-> -a 显示隐藏文件
-> 以列表形式显示文件和目录

# 显示一个文件的属性和文件所属的用户和组
ll

# 切换目录
cd
-> cd / 切换到根目录
-> cd ~ 切换到root目录
-> cd - 切换到上次访问的目录
-> cd .. 切换到上一级目录

# 查看当前文件的绝对路径
pwd

# 创建文件夹
mkdir

# 创建文件
touch

# 删除文件夹
rmdir

# 删除文件
rm

# 查找文件
find

# 修改文件内容
vim

# 根据名称查找文件路径：
find / -name 文件名

# 查看文件内容
cat

# vim查看文件
# 1.以vim进入文件
vim 文件名称
# 2.按下i进入插入模式
# 3.编辑文件
# 4.退出
-> 按下esc
-> 按下:wq 回车
-> w:保存文件
-> q:退出程序
```



## 2.文件属性

```bash
# 第一个字符代表文件类型：
d: 目录
-: 文件
l: 链接文档(link file)
b: 可供储存的接口设备
c: 装置文件里面的串行端口设备

# 接下来的字符代表文件权限，三个为一组
r: 可读
w: 可写
x: 可执行
-: 无该权限
```





## 3.防火墙指令

```bash
# 查看服务器防火墙端口：
firewall-cmd --zone=public --query-port=端口号/tcp

# 开放服务器防火墙端口：
firewall-cmd --zone=public --add-port=端口号//tcp --permanent

# 服务器防火墙端口刷新：
firewall-cmd --reload
```



## 4.yum指令

```bash
# 列出所有可更新的软件清单命令
yum check-update

# 更新所有软件
yum update

# 安装指定软件
yum install 包名

# 更新指定软件
yum update 包名

# 列出所有可安装的软件清单
yum list

# 删除软件
yum remove 包名

# 查找软件
search 包名
```



## 5.service指令

```bash
# 查看服务状态
systemctl status 服务名

# 开启服务
systemctl status 服务名 -l
-> l：展示日志

# 关闭服务
systemctl stop 服务名

# 设置服务开机自启动
systemctl enable 服务名

# 禁止服务开机自启动
systemctl disable 服务名
```



## 6.用户管理

```bash
# 修改用户
chown  #change owner

# 修改用户权限
chmod  #change mode

# 赋予当前用户root权限
输入su，然后输入密码

# 给用户赋予永久root权限
# 修改 /etc/passwd 文件，找到如下行，把用户ID修改为 0 ，如下所示：
chao:x:500:500:chao:/home/tommy:/bin/bash
——>
chao:x:0:500:chao:/home/tommy:/bin/bash
```



## 7.磁盘管理

```bash
# 列出文件系统的整体磁盘使用量
df -h  #disk full

# 检查磁盘空间使用量
du  #disk used

# 磁盘分区
fdisk
```



## 8.阿里云服务器

```bash
# 配置用户密钥对
# 1.创建密钥对
云服务器ECS->密钥对->创建密钥对->创建类型选择"导入已有密钥对"->填入本机的id_rsa.pub
# 2.将该密钥对与服务器绑定
# 3.重启服务器
# 4.使用ssh连接服务器
填入ip后不要填账号密码，选择添加key->选中本地id_rsa.pem->点击连接->输入用户名root->连接成功
```





## 9.其他

```bash
# nginx重启指令：
nginx -s reload

service配置文件路径：/etc/nginx/conf.d/
service网址资源路径：/usr/share/nginx/projects/

# 运行jar文件：
java -jar cblog.jar

# 指定端口运行jar文件：
java -jar -Dserver.port=8081 cblog.jar

# jar包的service文件地址：
/etc/systemd/system/cblog.service
```

