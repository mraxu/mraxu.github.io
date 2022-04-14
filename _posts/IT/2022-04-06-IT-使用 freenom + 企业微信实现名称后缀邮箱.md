---
layout: post
title:  邮箱
description: "无"
modified: 2022-04-06 10:20:20
tags: [IT]
post_type: developer
blogid: 20220406102020
categories: [IT]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:

---

# 使用 freenom + 企业微信实现名称后缀邮箱

### 1 注册freenom域名

- 网上教程很多, 不重复造轮子了

### 2 企业邮箱管理员注册

- [点击此处打开教程注册](https://service.exmail.qq.com/cgi-bin/help?subtype=1&&id=20012&&no=1001214)

- 注册完成之后打开下面这个界面

  ![Alt text]({{site.url}}/images/posts_image/i.png))

- 看到上面图片设置邮箱, 设置你注册的 freenom 账号

### freenom dns 解析设置

- > 引用官方教程
  >
  > STEP 1
  > \------
  >
  > For this, you first and foremost need to set the
  > name servers for your domain to the name servers of Freenom.
  >
  > You do this by:
  >
  > Go to My Domains
  > Click on Manage Domain
  > Click on Management Tools
  > Click on Nameservers
  > Select Use default nameservers
  >
  > Press Change Nameservers
  > DONE!
  >
  > STEP 2
  > \------
  > Now you can setup your DNS records, by going to
  > the Manage Freenom DNS area.
  >
  > You do this by:
  > Go to My Domains
  > Click on Manage Domain
  > Manage Freenom DNS
  >
  > Now you can enter a variety of different DNS records,
  > including A, MX and CNAME records.
  >
  > Extra remarks:
  >
  > \- You can use the 'name' field blank if you want to assign
  > a DNS record (like A record) to your entire domain
  >
  > \- For MX records, you need to add a priority. Simply type
  > in '10' (without quotes) in that field if you only have
  > one mail exchange (MX) server for your domain.
  >
  > It will take normally up to 30 minutes before name
  > server changes are distributed within our DNS servers.
  >
  > Thank you for using Freenom

  ![](https://gitee.com/axu8/pic-bed/raw/master/uPic/Snipaste_2022-04-07_15-10-49.png)
  
- 理论上你进行到这步骤就可以使用企业微信收发邮件了

### 3 等待 2-24 小时 MX 解析生效,

- 实测应该几十分钟或者十几分钟就可以了



### 4 实际收发测试

#### 4.1 使用 QQ 邮箱测试发送

![](https://gitee.com/axu8/pic-bed/raw/master/uPic/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_5f6b2cc9-2e0e-494b-9f7d-7c5c751cdbb6.png)

### 4.2 使用企业微信测试接收以及回复

![](https://gitee.com/axu8/pic-bed/raw/master/uPic/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_06543677-770a-49df-9a0a-c12d392ece1a.png)