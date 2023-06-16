- [MinIO](https://hub.docker.com/r/minio/minio) 
- [MinIO Docker Doc](https://min.io/docs/minio/container/index.html) 

## 1. Docker安装
```shell
docker run -d \
  --publish 9000:9000 \
  --publish 9001:9001 \
  --env MINIO_ROOT_USER=minioaccess \
  --env MINIO_ROOT_PASSWORD=miniosecret \
  --net dev \
  --restart=on-failure:3 \
  --name minio \
  minio/minio:RELEASE.2023-05-18T00-05-36Z server /data --console-address ":9001"

# 挂在目录及指定配置文件
docker run -d \
  --publish 9000:9000 \
  --publish 9001:9001 \
  --volume /etc/default/minio:/etc/config.env \
  --volume /mnt/data:/data \
  --env MINIO_CONFIG_ENV_FILE=/etc/config.env \
  --env MINIO_ROOT_USER=minioaccess \
  --env MINIO_ROOT_PASSWORD=miniosecret \
  --env MINIO_SERVER_URL=http://minio.example.net:9000\
  --net dev \
  --restart=on-failure:3 \
  --name minio \
  minio/minio:RELEASE.2023-05-18T00-05-36Z server /data --console-address ":9001"

docker exec -it -u root minio /bin/bash

docker container restart minio
```

- Account
  - minioaccess/miniosecret

[Console Dashboard](http://localhost:9001)
