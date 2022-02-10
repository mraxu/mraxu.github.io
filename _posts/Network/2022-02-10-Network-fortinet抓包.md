---
layout: post
title:  fortinet抓包
description: "无"
modified: 2022-02-10 10:20:20
tags: [Network]
post_type: developer
blogid: 20220210102020
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---

### 飞塔防火墙抓包
```
diagnose sniffer packet  any "host 101.37.21.61 and port 5060 " 4 0 l
```
### 飞塔防火墙设置源 IP
``` 
exe ping-s
```

### 飞塔防火墙流信息
```
diagnose debug flow filter addr 15.32.0.171 
diagnose debug flow filter addr 10.213.18.11
diagnose debug flow filter dport 12345
diagnose debug flow show function-name enable
diagnose debug flow trace start 100 
diagnose debug enable
```
### 清除流信息
```
diagnose debug flow filter clear
```

### 查看路由
```
get router info routing-table database
```