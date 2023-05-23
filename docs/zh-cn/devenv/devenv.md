开发环境搭建

# 一、软件列表
1. IDEA             zhile.io
2. DBeaver
3. MobaxTerm
4. VS Code
5. Maven            mvnrepository.com
6. JDK
7. Git
8. U Tools
9. Docker
10. Chrome
11. 企业微信\钉钉
12. FoxMail

# 二、软件安装
## 1. [IDEA](zhile.io)

1. Jrebel

```
GUID生成：https://www.guidgen.com/

激活URL :https://jrebel.qekang.com/GUID

激活成功后设置为离线模式
```

2. MyBatisCodeHelper-Pro


## 2. Git
```shell

git config --global user.name "liuhui"
git config --global user.email "hliu@pisx.com"

ssh-keygen -t rsa -C "hliu@pisx.com"
cat /c/Users/pisx/.ssh/id_rsa.pub

git init
git add .
git commit -m "Init project"
git remote add origin https://gitee.com/lorchr/spring-boot-samples.git
git branch --set-upstream-to=origin/master master
git push -u origin master
```

常用操作
```shell
-- 克隆仓库
git clone http://github.com/lorchr/spring-cloud-samples.git

-- 查看远程仓库地址
git remote -v

-- 移除远程仓库
git remote rm origin

-- 添加新的远程仓库地址
git remote add           cloud https://gitee.com/lorchr/spring-cloud-samples.git
git remote set-url --add origin http://github.com/lorchr/spring-cloud-samples.git
git push -u cloud master

# 提交
git push 仓库别名 分支 --allow-unrelated-histories
# 检出
git pull 仓库别名 分支 --allow-unrelated-histories
```

## 3. Docker更换软件源

修改Docker容器内部的软件源地址

1. 使用sed替换
    
    ```shell
    # 使用root用户执行命令行操作
    docker exec -it -u root <container-id(name)> /bin/bash

    # 查看软件源
    cat /etc/apt/sources.list

    # 替换软件源
    sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list
    sed -i "s@http://security.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list
    ```

如果使用的https源，则需要执行`apt install apt-transport-https`，再执行`apt update`更新源索引

2. 直接编辑 sources.list

    ```shell
    # 使用root用户执行命令行操作
    docker exec -it -u root <container-id(name)> /bin/bash

    # 查看系统版本
    cat /etc/os-release

    ## 追加
    cat << EOF >> /etc/apt/sources.list
    # Debian 10 buster

    # 中科大源

    deb http://mirrors.ustc.edu.cn/debian buster main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian buster-updates main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian buster-backports main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian-security/ buster/updates main contrib non-free

    deb-src http://mirrors.ustc.edu.cn/debian buster main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian buster-updates main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian buster-backports main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian-security/ buster/updates main contrib non-free

    # 官方源

    # deb http://deb.debian.org/debian buster main contrib non-free
    # deb http://deb.debian.org/debian buster-updates main contrib non-free
    # deb http://deb.debian.org/debian-security/ buster/updates main contrib non-free

    # deb-src http://deb.debian.org/debian buster main contrib non-free
    # deb-src http://deb.debian.org/debian buster-updates main contrib non-free
    # deb-src http://deb.debian.org/debian-security/ buster/updates main contrib non-free

    # 网易源

    # deb http://mirrors.163.com/debian/ buster main non-free contrib
    # deb http://mirrors.163.com/debian/ buster-updates main non-free contrib
    # deb http://mirrors.163.com/debian/ buster-backports main non-free contrib
    # deb http://mirrors.163.com/debian-security/ buster/updates main non-free contrib

    # deb-src http://mirrors.163.com/debian/ buster main non-free contrib
    # deb-src http://mirrors.163.com/debian/ buster-updates main non-free contrib
    # deb-src http://mirrors.163.com/debian/ buster-backports main non-free contrib
    # deb-src http://mirrors.163.com/debian-security/ buster/updates main non-free contrib

    # 阿里云

    # deb http://mirrors.aliyun.com/debian/ buster main non-free contrib
    # deb http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib
    # deb http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib
    # deb http://mirrors.aliyun.com/debian-security buster/updates main

    # deb-src http://mirrors.aliyun.com/debian/ buster main non-free contrib
    # deb-src http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib
    # deb-src http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib
    # deb-src http://mirrors.aliyun.com/debian-security buster/updates main
    EOF
    ```

3. 安装软件
   
   ```shell
    # 更新软件源
    apt-get update && apt-get upgrade -y

    # 安装apt-file
    apt-get install -y apt-file && apt-file update

    # 查找软件
    apt-file search /bin/ps | grep -w "bin/ps"

    # 安装软件
    apt-get install -y vim wget

    # Docker容器交互
    docker exec -it -u root <container-id(name)> /bin/bash
   ```

## 4. Redis Stream 基本命令 

- https://blog.csdn.net/qq_43956758/article/details/109860706

```lua
# 创建stream
XADD maintenance_order:event_alarm * type customIncident;

# 创建consumer group
XGROUP CREATE maintenance_order:event_alarm default_group 0;

# 获取stream元素个数
XLEN maintenance_order:event_alarm;

# 获取stream中所有元素 - 最小值 + 做大值
XRANGE maintenance_order:event_alarm - +;

# 获取stream信息
XINFO STREAM maintenance_order:event_alarm;

# 获取stream 的consumer group信息
XINFO GROUPS maintenance_order:event_alarm;

# 消费数据
XREADGROUP GROUP default_group default_consumer COUNT 1 STREAMS maintenance_order:event_alarm >;

# 删除消息
XDEL maintenance_order:event_alarm record_id;

# 删除stream
DEL maintenance_order:event_alarm;
```

Redis Lua脚本
```lua
-- 删除stream
DEL maintenance_order:event_alarm;

-- 设备告警
keys device_alarm_matching*
del device_alarm_matching:

-- 删除告警历史
keys thing_alarm_matching*
local keys = redis.call('keys', KEYS[1])
local temp = {}
for iter, value in ipairs(keys) do
    table.insert(temp, {value, redis.call('del', value) })
end
return temp
```

# Mysql
[Mysql](./Docker-Mysql.md ':include')

# Pgsql
[Pgsql](./Docker-Pgsql.md ':include')

# Redis
[Redis](./Docker-Redis.md ':include')

# InfluxDB
[InfluxDB](./Docker-InfluxDB.md ':include')

# EMQX
[EMQX](./Docker-EMQX.md ':include')

# Windows下Docker端口被占用的问题
[Docker port bind error in Windows](./windows-docker-port-bind-error.md)
