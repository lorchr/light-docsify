[EMQX](https://hub.docker.com/_/emqx)
```shell
docker run -d \
  --publish 18083:18083 \
  --publish 1883:1883 \
  --env HOCON_ENV_OVERRIDE_PREFIX=DEV_ \
  --env DEV_MQTT__ZONE__SHARED_SUBSCRIPTION=true \
  --env DEV_MQTT__ZONE__EXTERNAL__SHARED_SUBSCRIPTION=true \
  --env DEV_MQTT__BROKER__SHARED_SUBSCRIPTION_STRATEGY=round_robin \
  --env DEV_MQTT__BROKER__SHARED_DISPATCH_ACK_ENABLE=true \
  --restart=no \
  --name emqx \
  emqx:4.3

docker exec -it -u root emqx /bin/bash
vim /etc/emqx/emqx.conf

#修改这两个就行，默认配置文件里面就有，修改为utf8就行。
default-character-set=utf8
character-set-server=utf8
#这个不是必须的，设置character-set-server会自动设置这个
#collation-server=utf8_general_ci

```
- [Dashboard](http://localhost:18083)
  admin/public

## 共享订阅
关于[共享订阅](https://www.emqx.io/docs/en/v5.0/advanced/shared-subscriptions.html#shared-subscriptions-in-group)

1. 开启共享订阅
  
  ```conf
  # 开启共享订阅
  zone.shared_subscription = true
  zone.external.shared_subscription = true

  # 负载均衡策略 random round_robin sticky hash
  broker.shared_subscription_strategy = round_robin

  # 适用于 QoS1 QoS2 消息，启用后，当客户端离线时，将消息派发给订阅组内其他客户端
  broker.shared_dispatch_ack_enabled = true
  ```

2. 共享订阅的负载均衡策略

| 均衡策略    | 说明                         |
| ----------- | ---------------------------- |
| random      | 在所有订阅者中随机选择       |
| round_robin | 按照订阅顺序                 |
| sticky      | 一直发往上次选取的订阅者     |
| hash        | 按照发布者 ClientID 的哈希值 |

3. 关于Topic路径

```
$share/<group-name>/<topic-name>(/<topic-sub-name>)*
```

- $share : 共享订阅的标识
- group-name : 共享订阅的组别名称 group-name
- topic-name : 实际的topic名称
- topic-sub-name: topic名称，可以有多段组成

| 示例                          | 前缀   | 组别  | Topic 名称       |
| ----------------------------- | ------ | ----- | ---------------- |
| $share/abc/t/1                | $share | abc   | t/1              |
| $share/yunyi/01_混配/1#罐流量 | $share | yunyi | 01_混配/1#罐流量 |

**注意：**
- 在订阅Topic时，使用 `$share/<group-name>/<topic-name>`
- 在发送消息时，使用 `<topic-name>`，不需要带`前缀`及`组别`
