---
layout: post
title:  Ubuntu 18.04 无法打开网易云音乐窗口
description: 
modified: 2018-10-24 15:20:20
tags: [linux]
post_type: developer
blogid: 201810240001
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
## 问题描述

- 网易云版本 `1.1.0` 安装后点击图标无法启动，只能终端通过 `sudo netease-cloud-music`

## 原因

- 启动需要 `root`权限〔来自 stackoverflow〕，启动时需要启动单独的一个`sandbox`

##  解决办法

### 第一种办法

```
# 用 root 权限修改文件
sudo gedit /usr/share/applications/netease-cloud-music.desktop 
//如果提示 gedit 命令未找到，请用 apt-get install gedit〔Ubuntu〕
yum -y install gedit〔Centos〕
```

- 修改执行参数: 找到 `exec`那一行，在`%U`前面加上 --no-sandbox
- 修改完后保存，重启下系统。

###  第二种方法

```
sudo gedit /etc/sudoers
修改/etc/sudoers文件，加一行：
YOURNAME ALL = NOPASSWD: /usr/bin/netease-cloud-music
YOURNAME为你登录的用户名。
```

```
sudo gedit /usr/share/applications/netease-cloud-music.desktop 
修改Exec=netease-cloud-music %U 为 Exec=sudo netease-cloud-music %U, 这样点击网易云音乐图标就是以管理员权限启动的了，且不用输入密码。
```

