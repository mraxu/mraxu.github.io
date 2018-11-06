---
layout: post
title:  安装/升级到 Deepin 15.7 后不能使用 CrossOver 的解决方法
description: 
modified: 2018-11-06 15:20:20
tags: [linux]
post_type: developer
blogid: 201811060001
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
# 安装/升级到 Deepin 15.7 后不能使用 CrossOver 的解决方法

```
sudo apt-get install python-gtk2 # 安装相对应的库
cd /opt/cxoffice/bin/        #CrossOver的执行文件就在这个目录下
./crossover                  #启动CrossOver
```