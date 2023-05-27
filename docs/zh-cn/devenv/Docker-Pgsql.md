[Postgres](https://hub.docker.com/_/postgres)

## 1. Docker安装
```shell
docker run -d \
  --publish 5432:5432 \
  --env POSTGRES_PASSWORD=postgres \
  --restart=no \
  --name postgres \
  postgres:12.11

docker exec -it -u root postgres /bin/bash

docker container restart postgres
```

- Account
  - postgres/postgres