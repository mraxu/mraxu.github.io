---
layout: post
title:  使用Windows Diskpart进行分区
description: "这样分区更炫酷"
modified: 2018-1-11 13:20:20
tags: [Windows]
post_type: developer
blogid: 201801110001
categories: [Windows]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---

## Diskpart 命令简介
> Diskpart 命令是 Windows 环境下的一个命令，利用 Diskpart 可实现对硬盘的分区管理，包括创建分区、删除分区、合并（扩展）分区，设置分区后即刻生效，免去了重启电脑的操作。

---

> 正常运行该命令时需要系统服务的支持，所以在纯 DOS、XP 内核的 WinPE 环境下都是不能运行的，但是在 `Win7` / `Win8.1` / `Win10` 的预安装环境下却是可以的。利用 Diskpart 命令来分区，既不用借助第三方工具，也不会产生 100MB 的“系统保留”分区，其次分区操作直接设置即刻生效，不用重新启动计算机。

## 利用 Diskpart 命令分区

1. 当`Windows安装程序`运行到创建磁盘分区界面时按下 `Shift+F10` 启动命令窗口。
2. 输入 `Diskpart` 进入 Diskpart 的命令环境，其提示符为 `DISKPART>`
3. 在此提示下输入`相应命令`就可以进行分区操作，具体用到的命令有：
- Clean  
- List  
- Select  
- Create  
- Format  
- Exit
4. 使用 `List Disk` 命令显示的目标磁盘若为 1 号，则建立分区的步骤如下：以下是命令顺序及操作解释：
- List Disk：显示本机的所有磁盘，以便正确操作目标磁盘  
- Select Disk 1：选择 0 号磁盘  
- Clean ：清除 0 号磁盘上的所有分区  
- Create Partition Primary Size=512000 ：创建主分区，容量为：512000MB  
- Active：激活主分区  
- Format Quick：快速格式化当前分区  
- Create Partition Extended：创建扩展分区  
- Create Partition Logical Size=512000：创建逻辑分区一，容量为：512000MB  
- Format Quick：快速格式化当前分区  
- Create Partition Logical Size=512000：创建逻辑分区二，容量为：512000MB  
- Format Quick ：快速格式化当前分区  
- Create Partition Logical ：创建逻辑分区三，大小为剩余的容量  
- Format Quick ：快速格式化当前分区  
- Exit ：退出Diskpart命令环境  
- Exit ：退出命令窗口

**注**：以上命令都可以进行缩减,如:
-  **cre par pri size=512000**：*创建主分区，容量为51000MB*
- **for qui**：*快速格式化*
- **lis dis**：*显示磁盘列表*

## 思维导图版:
![Diskpart](https://i.imgur.com/3i9xyGS.png)