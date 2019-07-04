---
layout: post
title:  Linux 使用nmtui修改主机名以及IP
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
## 步骤1.修改主机名
 1. 终端里输入**nmtui**
 ![image](https://i.imgur.com/EhSXKYK.png)
 2. 选择`Set system hostname`![image](https://vgy.me/G417qh.png)
 3. 换成***Server2***![image](https://vgy.me/ZPoDTy.png)
 4. 再按***方向键↓***,选择**OK**
 5. 完成

## 步骤2.修改IP
1. 终端里输入**nmtui**
![image](https://i.imgur.com/EhSXKYK.png)
2. 选择***Edit a connect***
![gaga](https://vgy.me/zbqv6S.png)
3. 选择***eno***开头的网卡,然后**Edit**
![image](https://vgy.me/mow0Ks.png)
4. ![image](https://vgy.me/W1qwB0.png)
5. ![image](https://vgy.me/cQ83XH.png)
6. 设置IP完毕

## 步骤3.查看ip

1. 终端输入**ifconfig**或者**ip addr**
