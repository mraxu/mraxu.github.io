---
layout: post
title:  RAID 5 配置手册
description: "通过eRAID模拟器进行RAID 5的配置操作"
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

## 0.背景描述

- `RAID5`使用的范围
   - 随机数据传输，`安全性要求高`，如金融、数据库、存储等
   
## 1.名词解释

- **`Disk Group：磁盘组`，这里相当于是阵列，例如配置了一个RAID5，就是一个磁盘组** 
- **`VD(Virtual Disk):虚拟磁盘`，虚拟磁盘可以不使用阵列的全部容量，也就是说一个磁盘组可以分为多个VD**    
- **`PD(Physical Disk)`:物理磁盘** 
- **`HS(Hot Spare)`: 热备**
- **`Mgmt`：管理**
- **`Ctrl`: 控制**
- **`Total Free Capacity`:总可用容量**
- **`No Configuration Present!`:目前没有配置！**

## 2.技术原理

> 把`数据`和`相对应的奇偶校验信息`存储到组成`RAID5`的各个磁盘上，并且`奇偶校验信息`和`相对应的数据`分别存储于`不同的磁盘上`。当`RAID5`的一个磁盘数据`发生损坏`后，可以利用`剩下的数据`和`相应的奇偶校验信息`去恢复被损坏的数据。

## 3.技术特点
+ 有校验数据，提供数据容错能力校验值分散在各个硬盘
- RAID组中硬盘相当程度的分散了负载，高读取性能，中等写入性能
- RAID组同时仅允许一块硬盘故障，发生故障时，读写性能会下降
- 需要至少三块参数相同的磁盘组成，总容量为(N-1)*单盘容量

## 4.操作平台
- LSI RAID卡 
- `eRAID H810` 模拟器

## 5.操作步骤

1. 按照屏幕下方的虚拟磁盘管理器提示，在`VD Mgmt`菜单（可以通过`CTRL+P`/`CTRL+N`切换菜单），按`F2`展开虚拟磁盘
![](https://vgy.me/kcYPbi.png)

1.1. 在虚拟磁盘创建窗口，按`回车键`创建新虚拟磁盘
![](https://vgy.me/PzsaqK.png)

2. 确认`RAID`级别以后，按`下`方向键，将光标移至`Physical Disks`列表中，上下移动至需要`选择的硬盘位置`，按`空格键`来选择（移除）列表中的硬盘，当选择的硬盘数量达到这个`RAID级别`所需的要求时，`Basic Settings`的`VD Size`中可以显示这个`RAID`的默认容量信息。有`X`标志为选中的硬盘。 
选择完硬盘后按`Tab`键，可以将光标移至`VD Size`栏，`VD Size`可以手动设定大小，也就是说`可以不用将所有的容量`配置在`一个`虚拟磁盘中。如果这个`虚拟磁盘`没有使用我们`所配置的RAID5阵列`所有的容量，剩余的空间`可以配置`为另外的一个虚拟磁盘，但是配置`下一个虚拟磁盘`时必须返回`VD Mgmt`创建
![](https://vgy.me/IKtK5p.png)

3. 修改`高级设置`，选择完`VD Size`后，可以按`下`方向键，或者`Tab`键，将光标移至`Advanced Settings`处，按`空格键``开启/禁用`高级设置。
    - 如果`开启`后（红框处有`X`标志为开启），可以修改`Stripe Element Size`大小，以及阵列的`Read Policy`与`Write Policy，Initialize`处可以选择`是否在阵列配置的同时进行初始化`。
   - 高级设置默认为`关闭`（不可修改），如果没有`特殊要求`，建议`不要修改`此处的设置。
![](https://vgy.me/3rKBSO.png)

4. 配置Hot Spare有两种模式
   -   一种是`全局热备`，也就是指这个`热备硬盘`可以做为这个`通道`上所有阵列的`热备`；
   -   另一种是`独立热备`，配置`硬盘`为某个指定的磁盘组中的`所有虚拟磁盘做热备`，也就是说这个`磁盘组`以外的`其他阵列`即使硬盘掉线，这个`热备也不会去自动做rebuild配置全局热备`
- **热备相关**
 - ![](https://i.imgur.com/J7ujDDZ.png)
   - 在配置好的`虚拟磁盘管理界`下，将`光标移至`需要配置`独立热备`的`磁盘组`上，按`F2`键，在出现的菜单中选择 `Manage Ded. HS`
   - 
- ![](https://i.imgur.com/CQUgd49.png)
   - 将光标移至`3号`硬盘，按`F2`，在弹出的菜单中，选择`Make Global HS`，配置`全局的热备盘`
- **测试热备盘**
![](https://i.imgur.com/VCvnPZv.png)



