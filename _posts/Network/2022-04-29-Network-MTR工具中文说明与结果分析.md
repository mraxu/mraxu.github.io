---
layout: post
title:  MTR 工具使用说明与结果分析
description: "无"
modified: 2022-04-29 10:20:20
tags: [Network]
post_type: developer
blogid: 20220210102020
categories: [network ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---

## mtr 使用说明
```shell
mtr [-hvrctglspni46] [-help] [-version] [-report] [-report-cycles=COUNT] [-curses] [-gtk] [-raw] [-split] [-no-dns] [-address interface] [-psize=bytes/-s bytes] [-interval=SECONDS] HOSTNAME [PACKETSIZE]
常见可选参数说明：

    -r 或 -report：以报告模式显示输出。

    -p 或 -split：将每次追踪的结果分别列出来。

    -s 或 -psize：指定ping数据包的大小。

    -n 或 -no-dns：不对IP地址做域名反解析。

    -a 或 -address：设置发送数据包的IP地址。用于主机有多个IP时。

    -4：只使用IPv4协议。

    -6：只使用IPv6协议。

    另外，也可以在mtr命令运行过程中，输入相应字母来快速切换模式。

    ？或 h：显示帮助菜单。

    d：切换显示模式。

    n：切换启用或禁用DNS域名解析。

    u：切换使用ICMP或UDP数据包进行探测。
```
## 说明
默认配置下，返回结果中各数据列的说明如下。
```
    第一列（Host）：节点IP地址和域名。如前面所示，按n键可以切换显示。

    第二列（Loss%）：节点丢包率。

    第三列（Snt）：每秒发送数据包数。默认值是10，可以通过参数“-c”指定。

    第四列（Last）：最近一次的探测延迟值。

    第五、六、七列（Avg、Best、Wrst）：分别是探测延迟的平均值、最小值和最大值。

    第八列（StDev）：标准偏差。越大说明相应节点越不稳定。
```
![]({{site.url}}/images/posts_image/Snipaste_2022-04-29_14-44-06.png)