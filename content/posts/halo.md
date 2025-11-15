---
abbrlink: ''
author:
  name: GGhua
categories:
- 折腾
date: '2025-05-20T12:21:39+08:00'
draft: false
tags:
- Halo
title: Halo的部署安装
updated: '2025-11-15T15:11:49.451+08:00'
---
[使用 Docker Compose 部署 | Halo 文档](https://docs.halo.run/getting-started/install/docker-compose/?current=external-db)

```shell
mkdir ~/halo && cd ~/halo
```

docker-compase安装halo

```shell
~/halo/docker-compose.yaml
```

```yml
version: "3"

services:
  halo:
    image: registry.fit2cloud.com/halo/halo:2.19
    restart: on-failure:3
    network_mode: "host"
    volumes:
      - ./halo2:/root/.halo2
    command:
      # 修改为自己已有的 MySQL 配置
      - --spring.r2dbc.url=r2dbc:pool:mysql://172.21.80.1:3307/halo
      - --spring.r2dbc.username=root
      - --spring.r2dbc.password=Hxl@121314
      - --spring.sql.init.platform=mysql
      # 外部访问地址，请根据实际需要修改
      - --halo.external-url=http://localhost:8090/
      # 端口号 默认8090
      - --server.port=8090
```

启动服务

```shell
docker-compose up -d
# 查看日志
docker-compose logs -f
```

Docker CLI安装 halo

```sh
docker run -it -d --name halo -p 8090:8090 -v ~/.halo2:/root/.halo2 registry.fit2cloud.com/halo/halo:2.19
```
