[Mysql](https://hub.docker.com/_/mysql)

## 1. Docker安装Mysql 5.7
```shell
docker run -d \
  --publish 3306:3306 \
  --env MYSQL_ROOT_PASSWORD=admin \
  --env MYSQL_DATABASE=light \
  --env MYSQL_USER=light \
  --env MYSQL_PASSWORD=light \
  --restart=on-failure:3 \
  --name mysql5 \
  mysql:5.7

docker exec -it -u root mysql5 /bin/bash

mysql -u root -p

SHOW DATABASES;
USE mysql;
SELECT user, host, authentication_string, plugin FROM user;
CREATE USER 'light'@'%' IDENTIFIED BY 'light';
GRANT ALL PRIVILEGES ON *.* TO 'light'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

docker container restart mysql5
```

- Account
  - root/admin
  - light/light

## 2. Docker安装Mysql 8.0
```shell
docker run -d \
  --publish 3308:3308 \
  --env MYSQL_ROOT_PASSWORD=admin \
  --env MYSQL_DATABASE=light \
  --env MYSQL_USER=light \
  --env MYSQL_PASSWORD=light \
  --restart=on-failure:3 \
  --name mysql8 \
  mysql:8.0

docker exec -it -u root mysql8 /bin/bash

mysql -u root -p

SHOW DATABASES;
USE mysql;
SELECT user, host, authentication_string, plugin FROM user;
CREATE USER 'light'@'%' IDENTIFIED BY 'light';
GRANT ALL PRIVILEGES ON *.* TO 'light'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

docker container restart mysql8
```

- Account
  - root/admin
  - light/light

## 3. 配置
```shell
vim /etc/mysql/conf.d/mysql.cnf
```

```conf
[client]
default-character-set = utf8mb4

[mysql]
default-character-set = utf8mb4

[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
init_connect='SET NAMES utf8mb4'
# 设置表名大小写敏感
lower_case_table_names=0
```

1. lower_case_file_system: 当前文件系统是否大小写敏感（ON-敏感，OFF-不敏感），只读参数，无法修改
2. lower_case_table_names: 此参数不可以动态修改，必须重启数据库
   - 0 表名存储区分大小写，比较时区分大小写
   - 1 表名存储时转为小写，比较时不区分大小写
   - 2 表名存储区分大小写，比较时为转为小写