---
layout: post
title:  Linux DHCP 学习你急
description:
modified: 2019-07-04 15:20:20
tags: [linux]
post_type: developer
blogid: 2019107040001
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
## Linux DHCP

### dhcpd服务程序配置文件中使用的常见参数以及作用

| 参数                               | 作用                                                                                                              |
|:-----------------------------------|:------------------------------------------------------------------------------------------------------------------|
| ddns-update-style 类型             | 定义DNS服务动态更新的类型，类型包括：<br/>none（不支持动态更新）、interim（互动更新模式）与ad-hoc（特殊更新模式） |
| allow/ignore client-updates        | 允许/忽略客户端更新DNS记录                                                                                        |
| default-lease-time 21600           | 默认超时时间                                                                                                      |
| max-lease-time 43200               | 最大超时时间                                                                                                      |
| option domain-name-servers 8.8.8.8 | 定义DNS服务器地址                                                                                                 |
| option domain-name "domain.org"    | 定义DNS域名                                                                                                       |
| range                              | 定义用于分配的IP地址池                                                                                            |
| option subnet-mask                 | 定义客户端的子网掩码                                                                                              |
| option routers                     | 定义客户端的网关地址                                                                                              |
| broadcast-address 广播地址         | 定义客户端的广播地址                                                                                              |
| ntp-server IP地址                  | 定义客户端的网络时间服务器（NTP）                                                                                 |
| nis-servers IP地址                 | 定义客户端的NIS域服务器的地址                                                                                     |
| hardware 硬件类型 MAC地址          | 指定网卡接口的类型与MAC地址                                                                                       |
| server-name 主机名                 | 向DHCP客户端通知DHCP服务器的主机名                                                                                |
| fixed-address IP地址               | 将某个固定的IP地址分配给指定主机                                                                                  |
| time-offset 偏移差                 | 指定客户端与格林尼治时间的偏移差                                                                                  |

### 自动管理IP地址

- 模拟:“机房运营部门：明天会有100名学员自带笔记本电脑来我司培训学习，请保证他们能够使用机房的本地DHCP服务器自动获取IP地址并正常上网”。

#### 机房所用的网络地址以及参数信息

| 参数名称      | 值                           |
|:--------------|:-----------------------------|
| 默认租约时间  | 21600秒                      |
| 最大租约时间  | 43200秒                      |
| IP地址范围    | 192.168.10.50~192.168.10.150 |
| 子网掩码      | 255.255.255.0                |
| 网关地址      | 192.168.10.1                 |
| DNS服务器地址 | 192.168.10.1                 |
| 搜索域        | linuxprobe.com               |

#### 关闭虚拟机自带DHCP

![](https://www.linuxprobe.com/wp-content/uploads/2015/07/%E4%B8%8D%E4%BD%BF%E7%94%A8%E8%99%9A%E6%8B%9F%E6%9C%BA%E7%9A%84DHCP%E5%8A%9F%E8%83%BD.jpg)

#### 配置/etc/dhcp/dhcpd.conf

```
# 请注意，在配置dhcpd服务程序时，配置文件中的每行参数后面都需要以分号（;）结尾，这是规定
ddns-update-style none; # 不需要更新DNS
ignore client-updates; #忽略客户端更新DNS记录
subnet 192.168.10.0 netmask 255.255.255.0 { #作用域为192.168.10.0/24网段
range 192.168.10.50 192.168.10.150; #IP地址池为192.168.10.50-150（约100个IP地址）
option subnet-mask 255.255.255.0; # 定义客户端默认的子网掩码
option routers 192.168.10.1; # 定义客户端默认的网管地址
option domain-name "linuxprobe.com";# 定义默认的搜索域
option domain-name-servers 192.168.10.1; # 定义客户端的DNS地址
default-lease-time 21600; #定义默认租约时间（单位：秒）
max-lease-time 43200; #定义最大预约时间（单位：秒）
} #结束符,PS:跟一个循环结束符差不多
```

在**[红帽](https://www.linuxprobe.com/)**认证考试以及生产环境中，都需要把配置过的dhcpd服务加入到开机启动项中，以确保当服务器下次开机后dhcpd服务依然能自动启动，并顺利地为客户端分配IP地址等信息。真心建议大家能养成“配置好服务程序，顺手加入开机启动项”的好习惯：

```
[root@linuxprobe ~]# systemctl start dhcpd
[root@linuxprobe ~]# systemctl enable dhcpd
 ln -s '/usr/lib/systemd/system/dhcpd.service' '/etc/systemd/system/multi-user.target.wants/dhcpd.service'
```

#### 测试结果

把dhcpd服务程序配置妥当之后就可以开启客户端来检验IP分配效果了。重启客户端的网卡服务后即可看到自动分配到的IP地址

![](https://www.linuxprobe.com/wp-content/uploads/2015/07/DHCP%E8%87%AA%E5%8A%A8%E8%8E%B7%E5%8F%96IP%E5%9C%B0%E5%9D%80%EF%BC%88IP%E5%9C%B0%E5%9D%80%EF%BC%892.jpg)

PS:如果有兴趣，大家还可以再开启一台运行Windows系统的客户端进行尝试，其效果都是一样的。

### 绑定DHCP获取IP地址,比如老板必须要66或88的ip

#### 获取网卡MAC地址

![](https://www.linuxprobe.com/wp-content/uploads/2015/07/DHCP%E8%87%AA%E5%8A%A8%E8%8E%B7%E5%8F%96IP%E5%9C%B0%E5%9D%80MAC%E5%9C%B0%E5%9D%801.jpg)

#### 配置写法

|         host 主机名称 {          |
|:--------------------------------:|
| hardware ethernet 该主机的ip地址 |
|  fixed-address 你想指定的ip地址  |
|                }                 |

#### 老板不让你看主机信息咋整

我们首先启动dhcpd服务程序，为老板的主机分配一个IP地址，这样就会在DHCP服务器本地的日志文件中保存这次的IP地址分配记录。然后查看日志文件，就可以获悉主机的MAC地址了（即下面加粗的内容）。

```
[root@linuxprobe ~]# tail -f /var/log/messages
Mar 30 05:33:17 localhost dhcpd: Copyright 2004-2013 Internet Systems Consortium.
Mar 30 05:33:17 localhost dhcpd: All rights reserved.
Mar 30 05:33:17 localhost dhcpd: For info, please visit https://www.isc.org/software/dhcp/
Mar 30 05:33:17 localhost dhcpd: Not searching LDAP since ldap-server, ldap-port and ldap-base-dn were not specified in the config file
Mar 30 05:33:17 localhost dhcpd: Wrote 0 leases to leases file.
Mar 30 05:33:17 localhost dhcpd: Listening on LPF/eno16777728/00:0c:29:c4:a4:09/192.168.10.0/24
Mar 30 05:33:17 localhost dhcpd: Sending on LPF/eno16777728/00:0c:29:c4:a4:09/192.168.10.0/24
Mar 30 05:33:17 localhost dhcpd: Sending on Socket/fallback/fallback-net
Mar 30 05:33:26 localhost dhcpd: DHCPDISCOVER from 00:0c:29:27:c6:12 via eno16777728
Mar 30 05:33:27 localhost dhcpd: DHCPOFFER on 192.168.10.50 to 00:0c:29:27:c6:12 (WIN-APSS1EANKLR) via eno16777728
Mar 30 05:33:29 localhost dhcpd: DHCPDISCOVER from 00:0c:29:27:c6:12 (WIN-APSS1EANKLR) via eno16777728
Mar 30 05:33:29 localhost dhcpd: DHCPOFFER on 192.168.10.50 to 00:0c:29:27:c6:12 (WIN-APSS1EANKLR) via eno16777728
Mar 30 05:33:29 localhost dhcpd: DHCPREQUEST for 192.168.10.50 (192.168.10.10) from 00:0c:29:27:c6:12 (WIN-APSS1EANKLR) via eno16777728
Mar 30 05:33:29 localhost dhcpd: DHCPACK on 192.168.10.50 to 00:0c:29:27:c6:12 (WIN-APSS1EANKLR) via eno16777728
```

#### 往/etc/dhcp/dhcpd.conf写配置

```
[root@linuxprobe ~]# vim /etc/dhcp/dhcpd.conf
ddns-update-style none;
ignore client-updates;
subnet 192.168.10.0 netmask 255.255.255.0 {
range 192.168.10.50 192.168.10.150;
option subnet-mask 255.255.255.0;
option routers 192.168.10.1;
option domain-name "linuxprobe.com";
option domain-name-servers 192.168.10.1;
default-lease-time 21600;
max-lease-time 43200;
host linuxprobe {  #开始符号{该主机名称
hardware ethernet 00:0c:29:27:c6:12; #MAC地址
fixed-address 192.168.10.88; #你指定的ip
}
}
[root@linuxprobe ~]#systemctl restart dhcpd //重启服务
```

#### 客户端重启网卡服务测试

![](https://www.linuxprobe.com/wp-content/uploads/2015/07/%E7%BB%91%E5%AE%9A%E6%8C%87%E5%AE%9A%E7%9A%84IP%E5%9C%B0%E5%9D%801.jpg)
