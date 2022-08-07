---
layout: post
title: elastiflow 从零开始搭建
description: "无"
modified: 2022-8-1 10:20:20
tags: [Network]
post_type: developer
blogid: 20220801102020
categories: [network]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---

## 前言
使用 github 4.0.1 版本的 elastiflow 监控 H3C 的 sflow 协议
## 环境
- centos 7
- 4U+32G
## linux 命令

```
# centos 安装 docker
yum -y install docker
# centos 安装 docker-compose
curl -L "https://wood-bucket.oss-cn-beijing.aliyuncs.com/Linux/Docker/docker-compose-Linux-x86_64-1.29.1" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

## docker-compose 部署
### 创建 docker-compose.yml 文件
```
touch docker-compose.yml
```
- 复制下面的命令到 docker-compose.yml 文件
```
version: '3'

services:
  elastiflow-elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.8.1
    container_name: elastiflow-elasticsearch
    restart: 'no'
    ulimits:
      memlock:
        soft: -1
        hard: -1
      nofile:
        soft: 131072
        hard: 131072
      nproc: 8192
      fsize: -1
    network_mode: host
    volumes:
      # You will need to create the path and permissions on the local file system where Elasticsearch will store data.
      # For example...
      #   mkdir /var/lib/elastiflow_es && chown -R 1000:1000 /var/lib/elastiflow_es //这步一定要做
      - /var/lib/elastiflow_es:/usr/share/elasticsearch/data
    environment:
      # JVM Heap size
      #   - this should be at least 2GB for simple testing, receiving only a few flows per second.
      #   - for production environments upto 31GB is recommended.
      ES_JAVA_OPTS: '-Xms4g -Xmx4g'

      cluster.name: elastiflow

      bootstrap.memory_lock: 'true'

      network.host: 0.0.0.0
      http.port: 9200
      discovery.type: 'single-node'

      indices.query.bool.max_clause_count: 8192
      search.max_buckets: 250000

      action.destructive_requires_name: 'true'

  elastiflow-kibana:
    image: docker.elastic.co/kibana/kibana:7.8.1
    container_name: elastiflow-kibana
    restart: 'no'
    depends_on:
      - elastiflow-elasticsearch
    network_mode: host
    environment:
      SERVER_HOST: 0.0.0.0
      SERVER_PORT: 5601
      SERVER_MAXPAYLOADBYTES: 8388608

      ELASTICSEARCH_HOSTS: "http://127.0.0.1:9200"
      ELASTICSEARCH_REQUESTTIMEOUT: 132000
      ELASTICSEARCH_SHARDTIMEOUT: 120000

      KIBANA_DEFAULTAPPID: "dashboard/653cf1e0-2fd2-11e7-99ed-49759aed30f5"
      KIBANA_AUTOCOMPLETETIMEOUT: 3000
      KIBANA_AUTOCOMPLETETERMINATEAFTER: 2500000

      LOGGING_DEST: stdout
      LOGGING_QUIET: 'false'

  elastiflow-logstash:
    image: robcowart/elastiflow-logstash:4.0.1
    container_name: elastiflow-logstash
    restart: 'no'
    depends_on:
      - elastiflow-elasticsearch
    network_mode: host
    environment:
      # JVM Heap size - this MUST be at least 3GB (4GB preferred)
      LS_JAVA_OPTS: '-Xms4g -Xmx4g'

      # ElastiFlow global configuration
      ELASTIFLOW_AGENT_ID: elastiflow
      ELASTIFLOW_GEOIP_CACHE_SIZE: 16384
      ELASTIFLOW_GEOIP_LOOKUP: 'true'
      ELASTIFLOW_ASN_LOOKUP: 'true'
      ELASTIFLOW_OUI_LOOKUP: 'false'
      ELASTIFLOW_POPULATE_LOGS: 'true'
      ELASTIFLOW_KEEP_ORIG_DATA: 'true'
      ELASTIFLOW_DEFAULT_APPID_SRCTYPE: '__UNKNOWN'

      # Name resolution option
      ELASTIFLOW_RESOLVE_IP2HOST: 'false'
      ELASTIFLOW_NAMESERVER: '127.0.0.1'
      ELASTIFLOW_DNS_HIT_CACHE_SIZE: 25000
      ELASTIFLOW_DNS_HIT_CACHE_TTL: 900
      ELASTIFLOW_DNS_FAILED_CACHE_SIZE: 75000
      ELASTIFLOW_DNS_FAILED_CACHE_TTL: 3600

      ELASTIFLOW_ES_HOST: '127.0.0.1:9200'
      #ELASTIFLOW_ES_USER: 'elastic'
      #ELASTIFLOW_ES_PASSWD: 'changeme'

      ELASTIFLOW_NETFLOW_IPV4_PORT: 2055
      ELASTIFLOW_NETFLOW_UDP_WORKERS: 2
      ELASTIFLOW_NETFLOW_UDP_QUEUE_SIZE: 4096
      ELASTIFLOW_NETFLOW_UDP_RCV_BUFF: 33554432

      ELASTIFLOW_SFLOW_IPV4_PORT: 6343
      ELASTIFLOW_SFLOW_UDP_WORKERS: 2
      ELASTIFLOW_SFLOW_UDP_QUEUE_SIZE: 4096
      ELASTIFLOW_SFLOW_UDP_RCV_BUFF: 33554432

      ELASTIFLOW_IPFIX_UDP_IPV4_PORT: 4739
      ELASTIFLOW_IPFIX_UDP_WORKERS: 2
      ELASTIFLOW_IPFIX_UDP_QUEUE_SIZE: 4096
      ELASTIFLOW_IPFIX_UDP_RCV_BUFF: 33554432
```
- 静静等待 pull 镜像完成,即可完成部署

## H3C 命令
- [点此此处可以参考](https://www.h3c.com/cn/d_201907/1209848_30005_0.htm)
- 图 1-2 配置 sFlow 组网图
!()[https://resource.h3c.com/cn/201907/02/20190702_4353057_image002_1209848_30005_0.png]
```
3. 配置步骤
(1)       配置 IP 地址

请按照图 1-2 配置各接口的 IP 地址和子网掩码，具体配置过程略。

(2)       配置 sFlow Agent 和 sFlow Collector 信息

# 配置 sFlow Agent 的 IP 地址。

<Sysname> system-view

[Sysname] sflow agent ip 3.3.3.1

# 配置 sFlow Collector 信息：sFlow Collector 编号为 1，IP 地址为 3.3.3.2，端口号保持缺省值 6343，描述信息为 netserver。

[Sysname] sflow collector 1 ip 3.3.3.2 description netserver

(3)       配置 Counter 采样

# 在 FortyGigE1/0/1 上配置 Counter 采样的时间间隔为 120 秒，同时开启 Counter 采样功能。

[Sysname] interface fortygige 1/0/1

[Sysname-FortyGigE1/0/1] sflow counter interval 120

# 配置 sFlow Agent 输出 sFlow 报文的目的 sFlow Collector 编号为 1。

[Sysname-FortyGigE1/0/1] sflow counter collector 1

(4)       配置 Flow 采样

# 在 FortyGigE1/0/1 上配置 Flow 采样的采样模式为随机采样，并配置 Flow 采样的报文采样率为 4000，同时开启 Flow 采样功能。

[Sysname-FortyGigE1/0/1] sflow sampling-mode random

[Sysname-FortyGigE1/0/1] sflow sampling-rate 4000

# 配置 sFlow Agent 输出 sFlow 报文的目的 sFlow Collector 编号为 1。

[Sysname-FortyGigE1/0/1] sflow flow collector 1

4. 验证配置
# 显示 sFlow 的配置和运行信息。

[Sysname-FortyGigE1/0/1] display sflow

sFlow datagram version: 5

Global information:

Agent IP: 3.3.3.1(CLI)

Source address:

Collector information:

ID    IP              Port  Aging      Size VPN-instance Description

1     3.3.3.2         6343  N/A        1400              netserver

Port information:                                                              

Interface      CID   Interval(s) FID   MaxHLen Rate     Mode      Status

FGE1/0/1         1     120         1     128     4000     Random    Active

从上面的显示信息中可以看到开启 sFlow 功能的 FortyGigE1/0/1 接口处于 “Active” 状态，Counter 采样的时间间隔为 120 秒，Flow 采样的报文采样率为 4000，即在 4000 个报文中抽取一个
报文进行采样，表示 sFlow 功能正在正常运行。
```  
### 接口下取消监控命令
```
undo  sflow flow collector 
undo   sflow sampling-rate 
undo   sflow counter collector 
undo   sflow counter interval 
```
