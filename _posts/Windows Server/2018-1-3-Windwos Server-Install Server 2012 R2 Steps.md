---
layout: post
title:  Windows Server 2012 安装步骤
description: "使用VMware进行安装"
modified: 2018-1-3 15:20:20
tags: [Windows Server]
series: Windows Server系列文章
post_type: developer
blogid: 201801030002
categories: [Windows Server]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---

# Windows Server 2012 R2 安装步骤
## 1.准备系统安装盘
- 准备`Windows Server 2012 R2`镜像文件
  - 从[MSDN我告诉你](http://msdn.itellyou.cn)下载
  - **请用[迅雷](http://dl.xunlei.com/)下载**
- 使用`UltraISO`/`Rufus`制作安装启动盘
  - [UltraISO下载地址](http://www.upantool.com/plus/download.php?open=2&id=517&uhash=ba3d5e297a460492b1a967bf)
  - [Rufus下载地址](http://rufus.akeo.ie)
 

## 2.Data Backup「数据备份」
 - 如果机器为`全新安装`可以略过
 - 如果机器为`升级安装`:用`移动存储设备`将`重要数据`进行拷贝备份

## 3.BIOS Setting「BIOS设置」
- `R2`版本支持`UEFI Mode`或者`Legacy Mode`启动
  - 开机查看第一屏自检`左下角`通过什么按键进入`BIOS设置`
  - 设置`启动`模式:一般在`Boot`选项中的`Boot Mode`中选择`UEFI Mode`/`Legacy Mode`
  - 再次重启查看第一屏自检`左下角`通过什么按键进入`Boot Menu`**「启动菜单」**
  - 选择你所制作的`光碟`/`U盘`


## 4.创建RAID组
- 按`需求`/`预算`进行配置RAID`1`/`5`/ `6`/`10`/`50`
   - [RAID6配置指南](http://axu666.win/2017/12/27/RAID-6-%E6%93%8D%E4%BD%9C%E6%89%8B%E5%86%8C/)

## 5.安装Windows
- 输入[`产品密钥`](https://baike.baidu.com/link?url=Ugm5W5F0XFpEIwK9soKk1FmD2Ia_MQOxoqwladTWKvxeoFsll77QQSPlMrJcKY2MiNUMMRoAz7y_ysw984OaJiEJHjL5D4IJ-gkTrQgSO9RASFoRO_T0CNMkJIRfgYzH)
- 按照`需求`进行分区
- 选择`服务版本`,版本区别如下
  - `DataCenter`
    - 高等级虚拟化
    - 无限虚拟机部署
    - 所有功能
  - `标准版`
    - 低等级虚拟化
    - 2台限制虚拟机部署
    - 所有功能
- 一杯咖啡`等待安装完成`时间

## 6.驱动安装
`可选`: 
- 光盘安装
- 服务器官网`搜索主机号`安装
- 搜索已装`Server 2012设备管理器`出现感叹号的`硬件ID`进行安装

## 7.恢复备份
**通过`第二步`移动存储拷贝的重要文件,`Ctrl+C` `Ctrl+V`复制回已安装完系统的服务器`硬盘`内**