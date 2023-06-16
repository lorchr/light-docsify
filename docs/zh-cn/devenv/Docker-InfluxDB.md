[InfluxDB](https://hub.docker.com/_/influxdb)

## 1. Docker安装
```shell
docker run -d \
  --publish 8086:8086 \
  --env DOCKER_INFLUXDB_INIT_USERNAME=admin \
  --env DOCKER_INFLUXDB_INIT_PASSWORD=admin@123 \
  --net dev \
  --restart=no \
  --name influxdb \
  influxdb:1.8

docker run -d \
  --publish 8087:8086 \
  --env DOCKER_INFLUXDB_INIT_USERNAME=admin \
  --env DOCKER_INFLUXDB_INIT_PASSWORD=admin@123 \
  --net dev \
  --restart=no \
  --name influxdb1.7.8 \
  influxdb:1.7

docker run -d \
  --publish 8088:8086 \
  --env DOCKER_INFLUXDB_INIT_USERNAME=admin \
  --env DOCKER_INFLUXDB_INIT_PASSWORD=admin@123 \
  --net dev \
  --restart=no \
  --name influxdb1.8.4 \
  influxdb:1.8.4

docker exec -it -u root influxdb /bin/bash

# 修改配置
apt update && apt-get install -y vim

vim /etc/influxdb/influxdb.conf
[http]
  auth-enable=true

cat << EOF >> /etc/influxdb/influxdb.conf
[http]
  auth-enable=true
EOF

# 创建用户
influx

SHOW DATABASES;
USE _internal;
CREATE USER "root" WITH PASSWORD '123456' WITH ALL PRIVILEGES;
SHOW USERS;

# 重启使配置生效
docker container restart influxdb

# 查询版本
SHOW DIAGNOSTICS;
SHOW STAT;

# 查询tag字段和field字段
show tag keys from cpu

show field keys from cpu
```

- Account
  - admin/admin@123
  - root/123456


## 2. Windows安装InfluxDB及设置用户权限说明
### 安装Influxdb
1. 进入网址https://portal.influxdata.com/downloads/1.8

2. 将`influxdb`的zip压缩文件，解压到指定目录中
3. `管理员身份`运行cmd进入`influxdb`的文件夹内
4. 生成`influxdb`数据的默认配置config文件
  > 输入命令 `influxd config > influxd.config`

5. 编辑新生成的`influxd.config`文件，修改influxdb存放数据的路径

  ```shell
    [meta]	
      dir = "D:\\influxdb\\influxdatas\\meta"
      ···  ···  ···  ···
    [data]
      dir = "D:\\influxdb\\influxdatas\\data"	
      ···  ···  ···  ···
      wal-dir = "D:\\influxdb\\influxdatas\\wal"
  ```

6. 编辑完毕后护保存退出，在cmd内输入命令`influxd -config influxd.config`

7. 会输出 InfluxDB 的Logo，运行InfluxDB时不可关闭此命令窗口

8. 双击打开`influx.exe`文件，进行简单的操作。 输入 `SHOW DATABASES`

### InfluxDB增加用户及权限
1. 将`influxd.config`文件里，`auth-enabled = false`改为`true`
2. 关闭之前启动的`influxd.exe`命令窗口
3. 以管理员模式打开cmd窗口，重新进入`influxdb-1.x.x-1`的文件夹内
4. 输入启动服务命令`influxd -config influxd.config`
5. 双击打开`influx.exe`文件， 输入 `SHOW DATABASES`，如果报错说明身份认证功能已打开
6. 创建admin管理员用户`CREATE USER influxdb WITH PASSWORD 'influxdb' WITH ALL PRIVILEGES`
7. 验证账户是否创建成功，输入`auth`后按回车,根据提示输入用户名和密码。登录后输入`SHOW DATABASES`，如有输出数据库名称即为安装成功
