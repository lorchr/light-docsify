[InfluxDB](https://hub.docker.com/_/influxdb)
```shell
docker run -d \
  --publish 8086:8086 \
  --env DOCKER_INFLUXDB_INIT_USERNAME=admin \
  --env DOCKER_INFLUXDB_INIT_PASSWORD=admin@123 \
  --restart=always \
  --name influxdb \
  influxdb:1.8

docker run -d \
  --publish 8087:8086 \
  --env DOCKER_INFLUXDB_INIT_USERNAME=admin \
  --env DOCKER_INFLUXDB_INIT_PASSWORD=admin@123 \
  --restart=no \
  --name influxdb1.7.8 \
  influxdb:1.7

docker run -d \
  --publish 8088:8086 \
  --env DOCKER_INFLUXDB_INIT_USERNAME=admin \
  --env DOCKER_INFLUXDB_INIT_PASSWORD=admin@123 \
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
  admin/admin@123
  root/123456
