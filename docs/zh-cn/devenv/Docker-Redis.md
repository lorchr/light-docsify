[Redis](https://hub.docker.com/_/redis)
```shell
docker run -d \
  --publish 6379:6379 \
  --restart=no \
  --name redis \
  redis:6.2

docker exec -it -u root redis /bin/bash

wget https://raw.githubusercontent.com/redis/redis/6.2/redis.conf -O /usr/local/etc/redis/redis.conf

vim /usr/local/etc/redis/redis.conf

docker container restart redis
```

- Account
    /admin

```conf
# 绑定本机的IP地址，其他客户端只能通过该IP访问redis，本机多个网卡时，可以指定其中的一个或多个（空格分隔）
# bind 127.0.0.1              本机回环地址，只能本机访问
# bind 192.168.0.2 127.0.0.1  可以本机和 通过192.168.0.2 所属网卡访问（即同网段）
# bind * -::1                 通过本机所有的网卡访问
bind 192.168.0.2
# 设置密码
requirepass admin
#修改为守护模式
daemonize yes
# 关闭保护模式
protected-mode no
#设置进程锁文件
pidfile /usr/local/redis/redis.pid
#端口
port 6379
#客户端超时时间
timeout 300
#日志级别
loglevel debug
#日志文件位置
logfile /usr/local/redis/log-redis.log
#设置数据库的数量，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id
databases 8
##指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合
#save <seconds> <changes>
#Redis默认配置文件中提供了三个条件：
save 900 1
save 300 10
save 60 10000
#指定存储至本地数据库时是否压缩数据，默认为yes，Redis采用LZF压缩，如果为了节省CPU时间，
#可以关闭该#选项，但会导致数据库文件变的巨大
rdbcompression yes
#指定本地数据库文件名
dbfilename dump.rdb
#指定本地数据库路径
dir /usr/local/redis/db/
#指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能
#会在断电时导致一段时间内的数据丢失。因为 redis本身同步数据文件是按上面save条件来同步的，所以有
#的数据会在一段时间内只存在于内存中
appendonly no
#指定更新日志条件，共有3个可选值：
#no：表示等操作系统进行数据缓存同步到磁盘（快）
#always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全）
#everysec：表示每秒同步一次（折衷，默认值）
appendfsync everysec
```
