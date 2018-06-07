---
layout: post
title:  Windows10内置管理员无法运行程序
description:
modified: 2018-6-7 13:20:20
tags: [Windows]
post_type: developer
blogid: 201806070001
categories: [Windows]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
# 步骤一:
```
# 按win+R运行,输入
secpol.msc
```
# 步骤二:
- 双击打开`本地策略`，点击`安全选项`，接着找到`用户账户控制`，双击`以管理员批准模式运行所有管理员`。选择`已启动`，先点击`应用`最后重启就可以了。
