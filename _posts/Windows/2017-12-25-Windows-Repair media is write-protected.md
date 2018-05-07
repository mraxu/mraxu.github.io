---
layout: post
title:  修复介质被写保护
description: "利用软件进行介质修复"
modified: 2017-09-04 13:20:20
tags: [Windows,Diskmgmt]
post_type: developer
blogid: 201709040001
categories: [Windows]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---

## 问题
> * 今天收到同学的一张金士顿U盘
> * 问题是在Windows系统中使用时都是提示`介质写入保护`
## 解决思路
> - `系统自带磁盘管理器`格式化,提示完成格式化,介质写入保护
- `diskgennius`格式化,同上
- `Aomei分区助手`格式化,同上上
- 最终使用[Phison RestoreV3.23][1]软件进行修复,修复成功

## Phison Restore软件操作步骤
> - 解压刚下载的软件
> - 插入你出问题的磁盘
> - 运行压缩包内的`Restore_v3.23`
## 图片操作步骤
> ![][2]
![此处输入图片的描述][3]
![此处输入图片的描述][4]
## 修复完成的操作
> 如提示完成,请运行cmd,然后输入以下代码
**cmd开启步骤:**
Win+R-->输入cmd
```
chkdsk /f e:    
//e:是你需要修复完毕的驱动盘符
```

  [1]: http://www.usbdev.ru/?wpfb_dl=7609/ "软件链接"
  [2]: https://i.imgur.com/Lg4G9HR.png
  [3]: https://i.imgur.com/c9DPZIZ.png
  [4]: https://i.imgur.com/Qx2kODY.png