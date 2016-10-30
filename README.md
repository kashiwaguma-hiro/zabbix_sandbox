# zabbix_sandbox

zabbixの監視設定で遊んだ記録

# Dockerコンテナの説明

以下のコンテナを用意しています。

・zabbixサーバ
・zabbixが接続するDB
・監視対象
　・redis
　・rabbitmq(未設定)


# 手順
1.dockerイメージの準備

```bash
docker-compose build
```


2.起動
```bash
docker-compose up -d
```

3.起動確認
```bash
docker-compose ps
```

4.redisのzabbix_agentへの設定
TODO

5.rabbitmqのzabbix_agentへの設定
TODO

6.memcachedのzabbix_agentへの設定
TODO


# TODO
・redisのzabbixエージェント設定を自動化、またはイメージ配布
・memcachedのry


# 参考
https://github.com/rdvn/zabbix-templates
