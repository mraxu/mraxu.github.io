---
layout: post
title:  RedHat 7.0替换Centos源
description: "使用Redhat替换成Centos源"
modified: 2018-3-14 15:20:20
tags: [linux,Redhat]
post_type: developer
blogid: 201803140001
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
# RedHat7.0 替换Cent OS 源
## 前期准备
- ***yum文件下载*** 
  - [在这里下载](https://pan.baidu.com/s/1l-Ey3yKputoISVmq2-z1ZA) **提取码:mrxu**
- ***保证RedHat能联网***
```
[root@Server1 /]# ping www.baidu.com
PING www.a.shifen.com (183.232.231.172) 56(84) bytes of data.
64 bytes from 183.232.231.172: icmp_seq=1 ttl=51 time=13.8 ms
64 bytes from 183.232.231.172: icmp_seq=2 ttl=51 time=14.4 ms
```

## 安装步骤

1. 卸载`RedHat`自带的`yum`
```
rpm -aq | grep yum|xargs rpm -e --nodeps
```
2. 把在`百度云`下载的这五个rpm包下载到`Windows电脑`里，然后用`WinSCP`这个软件上传到redhat 7 系统里，`WinSCP`这个软件的使用方法就不在这里赘述了(如果是用`Vmware Workstation`虚拟出来的`Red Hat 7 ` 可以直接拖到虚拟机里的某一个目录)***如下↓***
![image](https://i.imgur.com/8zbR7Pk.png)
***之后用***
```
#转到根目录 
cd /
#安装所有「根目录」的yum包 
rpm -ivh yum-*
```
3. 新建`repo`配置文件

```
[root@Server1 ~]# vim /etc/yum.repos.d/CentOS-Base.repo
//复制以下内容到CentOS-Base.repo,之后按 :wq 保存并退出
#CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.
#
#
[base]
name=CentOS-$7 - Base - 163.com
#mirrorlist=http://mirrorlist.centos.org/?release=$7&arch=$basearch&repo=os
baseurl=http://mirrors.163.com/centos/7/os/$basearch/
gpgcheck=1
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
name=CentOS-$7 - Updates - 163.com
#mirrorlist=http://mirrorlist.centos.org/?release=$7&arch=$basearch&repo=updates
baseurl=http://mirrors.163.com/centos/7/updates/$basearch/
gpgcheck=1
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=CentOS-$7 - Extras - 163.com
#mirrorlist=http://mirrorlist.centos.org/?release=$7&arch=$basearch&repo=extras
baseurl=http://mirrors.163.com/centos/7/extras/$basearch/
gpgcheck=1
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$7 - Plus - 163.com
baseurl=http://mirrors.163.com/centos/7/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7
```
4. 清除缓存

```
[root@Server1 ~]# yum clean all
Loaded plugins: fastestmirror, product-id, subscription-manager
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
Cleaning repos: base extras updates
Cleaning up everything
```
5. 测试是否安装正常

```
[root@Server1 yum.repos.d]# yum -y install httpd
已加载插件：fastestmirror, product-id, subscription-manager
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
Loading mirror speeds from cached hostfile
正在解决依赖关系
--> 正在检查事务
---> 软件包 httpd.x86_64.0.2.4.6-67.el7.centos.6 将被 安装
--> 正在处理依赖关系 httpd-tools = 2.4.6-67.el7.centos.6，它被软件包 httpd-2.4.6-67.el7.centos.6.x86_64 需要
--> 正在处理依赖关系 /etc/mime.types，它被软件包 httpd-2.4.6-67.el7.centos.6.x86_64 需要
--> 正在处理依赖关系 libaprutil-1.so.0()(64bit)，它被软件包 httpd-2.4.6-67.el7.centos.6.x86_64 需要
--> 正在处理依赖关系 libapr-1.so.0()(64bit)，它被软件包 httpd-2.4.6-67.el7.centos.6.x86_64 需要
--> 正在检查事务
---> 软件包 apr.x86_64.0.1.4.8-3.el7_4.1 将被 安装
---> 软件包 apr-util.x86_64.0.1.5.2-6.el7 将被 安装
---> 软件包 httpd-tools.x86_64.0.2.4.6-67.el7.centos.6 将被 安装
---> 软件包 mailcap.noarch.0.2.1.41-2.el7 将被 安装
--> 解决依赖关系完成

依赖关系解决

==========================================================================================================================================================================================
 Package                                     架构                                   版本                                                    源                                       大小
==========================================================================================================================================================================================
正在安装:
 httpd                                       x86_64                                 2.4.6-67.el7.centos.6                                   updates                                 2.7 M
为依赖而安装:
 apr                                         x86_64                                 1.4.8-3.el7_4.1                                         updates                                 103 k
 apr-util                                    x86_64                                 1.5.2-6.el7                                             base                                     92 k
 httpd-tools                                 x86_64                                 2.4.6-67.el7.centos.6                                   updates                                  88 k
 mailcap                                     noarch                                 2.1.41-2.el7                                            base                                     31 k

事务概要
==========================================================================================================================================================================================
安装  1 软件包 (+4 依赖软件包)

总下载量：3.0 M
安装大小：10 M
Downloading packages:
警告：/var/cache/yum/x86_64/$releasever/base/packages/apr-util-1.5.2-6.el7.x86_64.rpm: 头V3 RSA/SHA256 Signature, 密钥 ID f4a80eb5: NOKEY               ]  0.0 B/s |    0 B  --:--:-- ETA 
apr-util-1.5.2-6.el7.x86_64.rpm 的公钥尚未安装
(1/5): apr-util-1.5.2-6.el7.x86_64.rpm                                                                                                                             |  92 kB  00:00:00     
httpd-2.4.6-67.el7.centos.6.x86_64.rpm 的公钥尚未安装                          86% [==========================================================-         ] 1.7 MB/s | 2.6 MB  00:00:00 ETA 
(2/5): httpd-2.4.6-67.el7.centos.6.x86_64.rpm                                                                                                                      | 2.7 MB  00:00:01     
(3/5): httpd-tools-2.4.6-67.el7.centos.6.x86_64.rpm                                                                                                                |  88 kB  00:00:00     
(4/5): mailcap-2.1.41-2.el7.noarch.rpm                                                                                                                             |  31 kB  00:00:00     
(5/5): apr-1.4.8-3.el7_4.1.x86_64.rpm                                                                                                                              | 103 kB  00:00:05     
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
总计                                                                                                                                                      567 kB/s | 3.0 MB  00:00:05     
从 http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7 检索密钥
导入 GPG key 0xF4A80EB5:
 用户ID     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 指纹       : 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 来自       : http://mirrors.163.com/centos/RPM-GPG-KEY-CentOS-7
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
警告：RPM 数据库已被非 yum 程序修改。
** 发现 2 个已存在的 RPM 数据库问题， 'yum check' 输出如下：
PackageKit-0.8.9-11.el7.x86_64 有缺少的需求 PackageKit-backend
rhn-check-2.0.2-5.el7.noarch 有缺少的需求 yum-rhn-plugin >= ('0', '1.6.4', '1')
  正在安装    : apr-1.4.8-3.el7_4.1.x86_64                                                                                                                                            1/5 
  正在安装    : apr-util-1.5.2-6.el7.x86_64                                                                                                                                           2/5 
  正在安装    : httpd-tools-2.4.6-67.el7.centos.6.x86_64                                                                                                                              3/5 
  正在安装    : mailcap-2.1.41-2.el7.noarch                                                                                                                                           4/5 
  正在安装    : httpd-2.4.6-67.el7.centos.6.x86_64                                                                                                                                    5/5 
  验证中      : mailcap-2.1.41-2.el7.noarch                                                                                                                                           1/5 
  验证中      : httpd-2.4.6-67.el7.centos.6.x86_64                                                                                                                                    2/5 
  验证中      : apr-util-1.5.2-6.el7.x86_64                                                                                                                                           3/5 
  验证中      : apr-1.4.8-3.el7_4.1.x86_64                                                                                                                                            4/5 
  验证中      : httpd-tools-2.4.6-67.el7.centos.6.x86_64                                                                                                                              5/5 

已安装:
  httpd.x86_64 0:2.4.6-67.el7.centos.6                                                                                                                                                    

作为依赖被安装:
  apr.x86_64 0:1.4.8-3.el7_4.1              apr-util.x86_64 0:1.5.2-6.el7              httpd-tools.x86_64 0:2.4.6-67.el7.centos.6              mailcap.noarch 0:2.1.41-2.el7             

完毕！
```
## 结语
`RedHat`的源跟`Centos`的源是可以共用的