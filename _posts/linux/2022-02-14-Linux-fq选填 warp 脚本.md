---
layout: post
title:  fq选填 warp 脚本
description:
modified: 2022-02-14 17:27:19
tags: [linux]
post_type: developer
blogid: 2019107040001
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
## fq 相关
### warp 跳过谷歌验证
```bash
wget -N --no-check-certificate https://cdn.jsdelivr.net/gh/kkkyg/CFwarp/CFwarp.sh && chmod +x CFwarp.s
```
### bbr 算法加速
```bash
wget -N --no-check-certificate "https://gist.github.com/zeruns/a0ec603f20d1b86de6a774a8ba27588f/raw/4f9957ae23f5efb2bb7c57a198ae2cffebfb1c56/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```
