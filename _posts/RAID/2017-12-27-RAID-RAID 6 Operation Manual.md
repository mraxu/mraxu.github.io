---
layout: post
title:  RAID 6 配置手册
description: "通过eRAID模拟器进行RAID 6的配置操作"
modified: 2017-12-27 15:20:20
tags: [RAID]
post_type: developer
categories: [RAID]
blogid: 201712270001
image:
  feature: posts_header/abstract-4.jpg
  credit:
  creditlink:
---








 RAID 6操作手册
===

## 名词解释
> - **`Disk Group`：磁盘组，这里相当于是阵列，例如配置了一个RAID5，就是一个磁盘组** 
> - **`VD(Virtual Disk)`虚拟磁盘，虚拟磁盘可以不使用阵列的全部容量，也就是说`一个磁盘组`可以分为`多个VD`**    
> - **`PD(Physical Disk)`物理磁盘** 
> - **`HS(Hot Spare)` 热备**
> - **`Mgmt`：管理**
> - **`Ctrl`: 控制**
> - **`Total Free Capacity`(总可用容量)**
> - **`No Configuration Present!`(目前没有配置！)**


## 背景描述

### 范围
> - **适用于`数据中心`，`信息中心`等对`数据安全级别要求比较高`的企业**

### 原理
> - **在`RAID-5`基础上增加`一位检验信息`,提供更好的`安全性`，允许坏两块盘**
> - **最终可用容量为`(N-2)x单盘容量`**

### 特点
> - **读取快,因多了一个校验盘,写入性能差**
> - **RAID控制器在设计上更加复杂，成本更高**



## 操作平台
> - **LSI RAID卡 `eRAID H810 模拟器`**
> - **最少4块硬盘**



## 操作步骤
> 1. 按照屏幕下方的虚拟磁盘管理器提示，在`VD Mgmt`菜单（可以通过`CTRL+P/CTRL+N`切换菜单），按`F2`展开虚拟磁盘创建菜单 
![image](https://i.imgur.com/5sAs0FW.png)
> 2.在虚拟磁盘创建窗口，按回车键选择`Create New VD`创建新虚拟磁盘
![image](https://i.imgur.com/lbByzKR.png)
> 3.在`RAID Level`选项按回车，可以出现能够支持的RAID级别，RAID卡能够支持的级别有`RAID 0/1/5/6/10/50`，根据具体配置的硬盘数量不同，这个位置可能出现的选项也会有所区别。
选择不同的级别，选项会有所差别。选择好需要配置的RAID级别（我们这里以`RAID6`为例），按`回车`确认。
![image](https://i.imgur.com/AkUjpZz.png)
> 4.确认RAID级别以后，按向下方向键，将光标移至`Physical Disks`列表中，`上下移动`至需要选择的硬盘位置，按`空格键`来选择（移除）列表中的硬盘，当选择的硬盘数量达到这个RAID级别所需的要求时，`Basic Settings`的`VD Size`中可以显示这个RAID的默认容量信息。有`X`标志为选中的硬盘。
选择完硬盘后按`Tab`键，可以将光标移至`VD Size`栏，VD Size可以`手动设定大小`，也就是说可以不用将所有的容量配置在一个虚拟磁盘中。
**注：各RAID级别最少需要的硬盘数量**
- RAID 0 = 1 
- RAID 1 = 2 
- RAID 5 = 3 
- RAID 6 = 4 
- RAID 10 = 4 
- RAID 50 = 6
![image](https://i.imgur.com/bk589jf.png)
> 5.修改高级设置，选择完`VD Size`后，可以按`下方向键`，或者`Tab键`，将光标移至`Advanced Settings`处，按`空格键`开启（禁用）高级设置
如果开启后（红框处有`X`标志为开启）
可以修改`Stripe Element Size`大小
以及阵列的`Read Policy`与`Write Policy`
`Initialize`处可以选择是否在阵列配置的同时进行初始化。
高级设置默认为关闭（不可修改），如果没有特殊要求，建议不要修改此处的设置。
![image](https://i.imgur.com/vYmhcOs.png)
6.上述的配置确认完成后，按`Tab`键，将光标移至`OK`处，按`回车`，会出现如下的提示，**如果是一个全新的阵列，建议进行初始化操作，如果配置阵列的目的是为了恢复之前的数据，则不要进行初始化。按回车确认即可继续。**
![image](https://i.imgur.com/Jv1TuJD.png)
7.配置完成后，会返回至`VD Mgmt`主界面，将光标移至图中`Virtual Disk 0`处，按`回车`。
![image](https://i.imgur.com/ECMUxgk.png)
> 8.可以看到刚才配置成功的虚拟磁盘信息，查看完成后按`esc键`可以返回主界面
![image](https://i.imgur.com/sWwmgsB.png)



## 注意事项
> - 如果是一个全新的阵列，建议进行初始化操作，如果配置阵列的目的是为了恢复之前的数据，则不要进行初始化。
> - 在生产环境中,请勿使用`Clear Config`
