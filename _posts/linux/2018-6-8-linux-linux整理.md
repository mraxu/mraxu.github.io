---
layout: post
title:  Linux旧知识整理
description: 整理归纳总结
modified: 2018-6-8 15:20:20
tags: [linux]
post_type: developer
blogid: 201806080001
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
# 1.Linux简介「了解」
- 1.1.Linux介绍
  - 是类Unix计算机操作系统的统称
  - 内核名字也是`Linux`
  - 是芬兰大学生Linus Torvalds于`1991年`编写的
  - Linux这个词本身只表示Linux内核,但在实际上人们已经习惯了用Linux来形容整个基于inux内核,并且使用`GNU`工程各种工具和数据库的操作系统

- 1.2.Linux发行版组成
  * Linux内核
  * 应用软件
    * 1.2.1.一些GNU程序库和工具
      * 1.Emacs集成开发环境和文本编辑器
      * 2.GCC语言编辑器
      * GNOME
    * 1.2.2.Shell
    * 1.2.3.图形桌面环境
      * KDE(qt编写)
      * GNOME(GTK编写)
      * Unity
    * 1.2.4.一些办公套件
      * OpenOffice
    * 1.2.5.编译器
      * gcc
      * g++
    * 1.2.6.文本编辑到科学工具的应用软件
      * vi
      * gedit
- 1.3.Linux版本
  * 商业公司维护的发行版本「Redhat」系列
    * RHEL「Redhat Enterprise Linux」也就是所谓的Redhat Advance Server「收费version」
    * Centos「Redhat社区克隆版,免费」
    * FedoraCore「由原来的Rethat桌面版本发展而来,免费」
  * 社区组织维护的发行版本Debian系列
    * Debian
    * Ubuntu
    * 其他发行版可详细查询[distrowatch](http://distrowatch.com/)和[Linux distrowatch Timeline](https://en.wikipedia.org/wiki/File:Linux_Distribution_Timeline.svg)

# 2.Linux目录结构
- 2.1.根目录结构
  - `dev:`设备文件所在目录「device的缩写」
  - `etc:`包含了当前操作系统用户所有配置的相关信息
  - `home:`当前操作系统所安装的用户的主目录
  - `lib:`操作系统使用的库文件以及相关的配置都放在此目录下
  - `mnt`一般为手动挂载的目录
  - `media`一般为系统自动挂载的目录
  - `usr`unix软件资源包管理目录,存放的是当前用户下的一些东西
  - `bin`Linux操作系统下可以执行的系统级的二进制命令「binary简称」
  - `sbin`超级用户需要用到的二进制命令存储在该目录下「super binary简称」
  - `boot`系统在开机的时候需要加载的一些文件和配置
  - `lost+found`存放系统错误产生的文件碎片,方便用户查找和恢复
  - `proc`内核提供的一个接口,主要用来存储系统统计信息
  - `root`root用户的宿主目录

- 2.2.目录路径介绍
  - `绝对路径`:从根目录开始描述的路径,也就是从 "/" 开始
  - `相对路径`
    - 从当前位置开始描述的路径
    - `.`表示当前目录
    - `..`表示当前目录的上一级目录
    - 两个临近目录直接进行切换,命令:`cd -`
- 实例
**xuguojing@xuguojinglinux:~$**
- 1.第一个xuguojing:当前登录的用户
- 2.@:英文at的意思,表示在
- 3.第二个xuguojinglinux:表示主机名「hostname」
- 4.~:当前工作目录的位置:宿主目录
- 5.$:表示当前登录的用户为普通用户,如果是`#`则为超级用户
