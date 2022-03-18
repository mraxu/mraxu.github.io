---
layout: post
title:  华为 eSight
description: "无"
modified: 2020-06-06 10:20:20
tags: [Network]
post_type: developer
blogid: 20200606102020
categories: [Network]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---

# 华为路由与交换 eSight基本概述学习笔记

2020-06-06 18:34:30

随着网络技术的飞速发展，企业网中网络设备的数量成几何级数增长，网络设备的种类也越来越多，企业网络的结构越来越复杂，里边常常会包含来自不同厂商的多种网络设备，如果每种设备都使用与之相配套的网管平台来管理的话，这就使得企业网络的管理变得十分复杂。

为此，华为推出新一代面向企业网络的运维管理系统eSight，实现对不同种类和厂商的网络设备进行统一管理，网络和业务的快速部署与维护，大大提升了网络的管理效率。那eSight相对其他网管软件都拥有什么优势？它是如何进行安装和部署的？

esight的安装耗损的硬件资源是比较高的，普通的笔记本根本就运行不起来，搞服务器操作系统应该是win2008就可以，服务器版本。

esight 是华为公司推出的新一代面向企业有线/无线园区，企业分支网络还是数据中心网络的运维管理系统，能够实现对企业资源、业务、用户的统一管理及智能联动

这个网管系统可以去管理企业里边，路由器，交换机,AP,AC，然后服务器，也可以去管理分支机构的，路由器和交换机，甚至是第三方的路由器和交换机，都是可以的，对于这个esight，它有三个版本，不同的版本提供的功能不一样，可以适用不同的企业规模，规模大一点就用一个高版本，规模小一点，就简单就行了，三个版本分别叫做精简版，标准版（wlan的管理，AP,AC做管理的话，需要用标准版，网络流量的分析，mpls 都需要标准版，qos的管理，），专业版（支持数据中心的管理，包括linux的双机热备管理，如果是在数据中心，）。一个比一个功能更加丰富。每种的版本的费用肯定是不一样的，因为这个esight不是免费的软件，下载了软件之后，还有license的申请，向华为去购买这个license的。

## **企业网络管理的诉求** **-** **设备数量增长**

##  ![img](https://img-blog.csdnimg.cn/20200605140704194.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



随着设备数量的增加，网络管理的复杂性也相应提高，这就意味着需要更多的维护支撑人员，增加了设备维护成本，所以就需要一个支持大规模、便捷管理的网管平台。 

从之前学习的内容可以看出来，在我们的日常工作中，我们都是通过命令行来管理我们的路由器，交换机之类的，命令行管理也是可以的，但是，当网络规模扩大的时候，管理大中型企业的网络的时候，网络中的设备有几百个，上千个，这时候大家会碰到一个问题，一个比较常见的问题，日常网络在管理的时候，其实是没办法了解网络哪里出现了问题的，所以我们最长碰到的一个问题就是，如果网络哪里故障了，网络管理员不是第一个知道的，而是下面出故障的那个用户，他是第一个知道的，然后用户会往上报告说，这边网络出现故障了，这样的话，你再去管理，去排错。这样的方式，明显，大家的使用体验会很差，网管的作用没有完全发挥出来，这个就是网络管理中，如果用传统的命令行管理的话，没有办法掌握全局的网络的动态。

## **企业网络管理的诉求** **-** **多厂商统一管理** 

![img](https://img-blog.csdnimg.cn/20200605141604258.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

每引入一家厂商的网络设备，就需要引入配套的厂商网管，而目前的厂商网管仅能管理自己厂商的设备，且每个厂商网管的操作界面、管理内容等均不相同，所以要实现对全网进行高效地统一管理，就需要使用一种标准、通用的网络管理协议。

还有一个问题就是目前网络设备，虽然厂家并不是特别多，但是由于网络标准可以互通，所以网络中的设备并不是一个厂商的，很有可能在一个公司里边，它的设备并不是只有华为的设备，还有其他厂商的设备，这些设备之间是可以互通的，虽然可以通过命令行登进去，命令行肯定也有微小的差别，如果说一个华为的网管系统只能管华为的设备，然后中心的网管系统只能管中心的设备，那么这样的话，这整个网络不久碎片化了，我想看一个整个网络的拓扑，我还得不停的更换网管系统吗？所以一般来说，希望一个网管系统可以把所有厂商的设备都给管理起来，起码可以在一个网管系统上看到一个非常完整的网络拓扑。

那么华为推出了eSight，这个eSight是这个华为的网管的名字也是他的注册商标。

##  **华为****eSight****企业运维解决方案**

eSight系统是华为公司研制的新一代面向企业网络园区、企业分支的运维管理系统，主要关注点就是这个ip网络，实现对企业资源、业务、用户的统一管理等功能。

特点一：轻量级系统，向导式安装；免客户端，通过浏览器随时随地管理网络。

华为的esight在安装的时候，特别简单，跟平时的应用软件安装一样，如果是windows的话，装上去之后，就会有一个安装界面出来，然后填一些必须的参数，选一些选项，然后，就一直点下一步就好了。

免客户端的话，就是说，华为的esight是一个B/S系统，就是在安装的时候，在机房里安装一个服务器，这台服务器就是网管工作站（NMS），通过这个NMS去管理网络设备，但是一个网管人员要去查看网络设备的时候，是不需要跑到这个网管工作站上去的，完全可以在自己的办公室，办公桌的pc机，用浏览器把它打开，NMS相当于提供了一个网站。用浏览器打开这个界面之后，可以看到整个拓扑的情况了，看到这个网络设备的情况了。

通过浏览器随时随地管理网络，不管你人在哪里，只要你能接入到企业的网络，就都可以去进行一个管理了。

特点二：面向不同客户提供相应的解决方案。

esight提供了不同的版本，一个是精简版，这个版本可以免费的下载，可以试用一下，用的比较多的是标准版，广大的企业一般会用到这个，专业版，节点数量更多，适用于一些有总部和分部的那种公司，这个专业版和标准版，最大的区别在于分级管理，分公司归分公司管，总部管分公司的，就是这样的分级管理方式

特点三：多厂商统一管理，采用被广泛使用的标准网络管理协议SNMP。

这个管理协议，是IETF标准定义的，只要是兼容这个SNMP的设备，其实都可以通过这个esight去管理，那么现在不管是哪个厂商生产的设备都是支持这个SNMP这个协议的，

| **版本**           | **管理规模** | **适用场景**                                     |
| ------------------ | ------------ | ------------------------------------------------ |
| 精简版             | 60节点       | 满足小规模的网络监控场景                         |
| 标准版（主流应用） | 0-5K节点     | 满足大部分网络管理需求，提供全方位的网络业务管理 |
| 专业版             | 0-20K节点    | 提供对超大型网络进行分级管理                     |



eSight可管理的设备：

eSight 提供了灵活的第三方设备管理能力。预适配华为、 H3C 、 CISCO 、中兴等厂商的网络设备，以及 IBM 、 HP 、 SUN 等厂商的 IT 设备 。

对于支持标准 MIB （ RFC1213-MIB ， Entity-MIB ， SNMPv2-MIB ， IF-MIB ）的第三方设备， eSight 通过自定义设置就能达到与预置的第三方设备同样的管理能力 。

对于不支持标准 MIB 的第三方设备，可以通过打网元补丁的方式进行适配 。

eSight 是如何与被网管设备之间进行通信的呢？

## **简单网络管理协议****SNMP** 

SNMP的结构包括网管站NMS（Network Management Station）和Agent两部分。SNMP就是规定NMS和Agent之间如何传递管理信息的应用层协议。 

这个NMS一般是在机房环境中的，人在机房，也可以在办公室，用浏览器去管，去看这个NMS上的一些信息，然后这个网管工作站，是通过SNMP(简单网络管理协议)去管理网络中的设备，agent和MIB是同一个系统里边的，可以把他们看成存在在一台路由器里边，事实上像其他的厂商的设备也是网管工作站，通过snmp去管理网络中的设备，这个里边分了两个结构，一个是agent，这个agent可以把它理解成是一个软件，这个路由器要跟网管工作站进行通信，肯定是需要有协议的，但是肯定是需要有个软件去操作这个包，还有就是要取数，在路由器的本地也是有一个数据库的，这个数据库叫做管理信息数据库，MIB management information base，这个库里边包含了很多数据，端口的状态，流量，ip地址，运行的各种协议，邻居状况，版本信息，等等一些参数，如果网管工作站通过这个协议要获取一些数据的时候，这个angent就会，去负责沟通，然后，去这个数据库里取数，取完数之后，报告给工作站。这个agent这个软件跟mib实在一台设备上，然后其他的设备上也是一样的，如果要取得全网的状态，那么每个设备都需要进行描述的。

![img](https://img-blog.csdnimg.cn/20200605150618429.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

NMS （ Network Management System ）是运行在网管端工作站上的网络管理软件。网络管理员通过操作 NMS ，向被管理设备发出请求，从而监控和配置网络设备。

SNMP 的版本：

SNMPv1 ：方便实现，安全性弱。

SNMPv2c ：有一定的安全性，现在应用最为广泛。

SNMPv3 ：定义了一种管理框架，引入了 USM （ User Security Model 用户的安全模型），为用户提供了安全的访问机制。

Agent ：运行在被管理设备上的代理进程。被管理设备在接收到网管设备侧 NMS 发出的请求后，由 Agent 作出响应操作。主要功能包括：收集设备状态信息、实现 NMS 对设备的远程操作、向网管端发出告警消息。

MIB ：是一个虚拟的数据库，是在被管理设备端维护的设备状态信息集。 Agent 通过查找 MIB 来收集设备状态信息。 MIB 按照层次式树形结构组织被管理对象，并使用 ASN.1 格式进行描述。



这个管理信息的数据库，每台设备上都有，但是，它的组织方式，跟我们平时见到的关系型数据库不太一样，它的组织方式是一个树形的，是一颗树，每颗树的分叉都有一个值，如果要取一个分支上的参数的时候，如果要取图上的这个5的参数的时候，取的时候就是1.2.1.1.5，这个树上的这个5的这个标识就是这个1.2.1.1.5

SNMP这个协议是用来沟通的，然后这个agent是用来执行的一个软件，取数是这个mib库，这个库的组织是树形来进行描述的，这个库是怎么取组织的，定义了一些标准库，有MIB II,RMON，这是当前市场上能看到的网络设备，都会支持，然后把不同的厂商都会按照不同的思路，还构建了自己的私有库，就是说这颗树上的有一些分支是专门定义好了，这是你厂商的私有库，当然华为也有自己的分支，华为自己的分支，就都在这里面。这个厂商的私有库都是厂商自己定的，但是厂商都会放出来的，如果你要让你的网管工作站也去支持这些私有库，那么你就要去相应的厂商里边，下载它相应的mib库的分支的组织方式，了解它的数据是怎么组织的。

## **SNMP****报文交互过程** 

![img](https://img-blog.csdnimg.cn/20200605150740489.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

这个交互过程并不是顺序的，网管工作站发送的，get request就是取数，取你的某个数值，然后通过response就把你要的数据给你发送过来了，Get-Next-Request取下一个数值，然后把下一个数值给取过来了，Get-Next-Request必须跟在get reques 之后，Set-Request就是给这个设备进行配置，比如说要把哪个设备的端口给关闭了，就通过这个Set-Request去shutdown，这个是Set-Request，前面两个操作呢，是属于读，后面这个Set-Request是属于写的，trap这个操作是特殊的，发起方是被管设备主动发起的，主动的告诉网管工作站发生了哪些事情，告知设备上发生的紧急事件，（链路dawn了）

SNMP版本有v1 v2c v3版本

v2版本多了块的操作就是可以批量的读取一些数据，

v3的话，增强课网管的权限和安全控制，跟其他协议一样，ip协议在发送的时候是明文的方式去发送的，所以相对来说并不是很安全，v1和v2的认证很简单，其实就是个字符串，还是以明文发送的，v3的版本增加了安全，传送过程是加密的，第二个是做了权限的控制，可以控制你只能访问某个树的某个分支，



SNMPv1 定义了 五 种协议 操作：

Get-Request ： NMS 从代理进程的 MIB 中 提 取一个或多个参数值。

Get-Next-Request ： NMS 从代理进程的 MIB 中按照字典式排序 提 取下一个参数值。

Set-Request ： NMS 设置代理进程 MIB 中的一个或多个参数值。

Response ：代理进程返回一个或多个参数值。它是前三种操作的响应操作。

Trap ：代理进程主动 向 NMS 发送报文，告知 设备上 发生的紧急或重要事件。



网管工作站这边肯定也是需要去配置的，那在这个网管工作站这边，它要管理哪个设备，肯定是要把这个设备放进去，把这个设备的管理地址放进来，如果是v1，v2的话，还有一个管理的口令也需要写进去，这个口令有一个专门的名词叫做团体属性，就是这个管理的community需要写进去，

在路由器里也是一样，

##  **路由器****SNMP****基本配置流程**

![img](https://img-blog.csdnimg.cn/20200605150831820.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

首先需要开启设备的snmp agent功能， 启用之后需要配置snmp的协议版本，这个协议的版本，如果说对于安全性没有那么高的要求的话，可以用版本2，然后配置读写团体名，前面两个参数是读，后面一个是写，读写的口令设置完，如果在服务器端需要导入这个设备的时候，也要把它写上去，这样它才能在这个设备上去取数，最后有一个trap，可以不设置，如果不让设备主动报告的话，也可以，如果你希望这个设备在发生紧急情况的时候，主动报告，那你就要配置了，需要配置这个trap参数，配置这个设备发送告警和错误码的目的主机，你得知道发生紧急情况的时候，往哪个主机发，往网络管理员的主机的ip地址去发，后面的联系方式就是一个说明文件，方便后来的管理员可以看见

## **路由器****SNMP****基本配置** 

![img](https://img-blog.csdnimg.cn/20200605150906856.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

操作步骤

（可选）执行命令 snmp -agent ，启动 SNMP Agent 服务。

缺省情况下， SNMP Agent 服务开启。执行任意 snmp -agent 的配置命令（无论是否含参数）都可以触发 SNMP Agent 服务启动，故该步骤可选。

执行命令 snmp -agent sys-info version v2c ，配置 SNMP 的版本信息为 SNMPv2c 。

执行命令 snmp -agent community { read | write } community-name [ mib -view view-name | acl acl -number ] ，配置设备的读写团体名，并通过选择是否配置 mib -view view-name 或 acl acl -number ，限制网管对设备的访问权限。

配置读写口令的时候，不建议用缺省的，很容易被人猜中，这个口令可以查看哪个分支，iso-view ，如果不需要trap，配置到第五条就可以了，如果配置trap就得往后配置一些参数，发这个报文的目的地址，源地址，还有一些其他的参数，

网管系统上也需要配置，我这台路由器是需要被管理的。

## **安装盘介绍** 



eSight 安装可以安装在windows和SUSE Linux上，安装过程支持静默安装也就是说，这个过程中没有用户交互的，支持的语言是中文英文两种，系统采用B/S架构，安装完网管工作站NMS之后，后续的网络工作管理，不需要到网管工作站，可以通过浏览器登进去就可以了。安装的时候，可以不装License，在后续给他导进去就可以了。

功能：

支持 windows 和 SUSE Linux 两套安装盘；

安装过程支持静默安装；没有报文交互的

支持中文和英文两种语言；

系统采用 B/S 架构，客户端免安装；

安装过程与 License 无关，安装完成后由用户自行导入。

性能：

各版本安装盘最大不超过 850M ；（不成为安装的限制条件）

安装时间不超过10 分钟。



eSight有两种安装方式：光盘安装和软件包安装。 

## **安装流程**

（华为提供两种安装方案，一个是已经给你安装好了，华为也有自己的服务器，如果想省心一点的话，就连服务器，连安装包装好，直接一个硬件服务器买回来架上去就好了，还有一个就是自己买硬件服务器，来安装这个网管软件，自己安装的流程，可以参考下面的这个流程。）

预安装方案：华为公司发货的服务器已经进行预安装，包括操作系统和 eSight 系统的安装。 

全新安装方案：如果是自购服务器，或需要重新安装 eSight 系统，请参考下面的安装流程。

（硬件准备好，然后安装操作系统，网管是需要数据库的，所有的网管软件都需要数据库，这个数据库是用来，存储从设备上取来的数据的，通过SNMP从路由器上取来的数，在网管系统上是需要有数据库存的，安装好数据库之后，安装eSight，然后安装防病毒软件，安全加固这些东西，然后导入CA证书，网管可以通过浏览器去访问，但是这个访问是HTTPS,是加密的，加密的访问是需要证书的，这个时候需要有CA证书，然后是启动eSight这个服务，启用之后就可以进行登录了，这个license可以最后单独加载，不用安装的时候加载。）

![img](https://img-blog.csdnimg.cn/202006060019318.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



安装防病毒软件： eSight 配套的防病毒软件推荐采用趋势科技防毒墙网络版 ( OfficeScan ) ，用户可以在购买 eSight 产品的同时购买 OfficeScan 防病毒软件。

导入 CA 证书：

安全证书是一种数字证书，用于在客户端浏览器和 Web 服务器之间建立一条安全通道，通道中的数据通过加密算法进行加密。

自签名证书和 CA 证书区别：

自签名证书： eSight 安装过程中临时生成的安全证书，以保证 eSight 安装完成后能够正常运行。获取方式： eSight 安装过程中会自动生成。

CA证书：由正式机构颁发的安全证书。获取方式：需要向正式机构申请。

## **系统安装软硬件环境介绍**

这个硬件环境跟我们要管理的硬件数量有关，每个设备它的数据取上来，是需要一定的存储空间的，这个设备的数量越多，这个存储空间也要越大，放到数据库里边，存储空间肯定要越大，还有一个就是每个设备要取数，肯定需要一定的操作，每个设备多少取去一点，这个操作的动作就越多，所有性能的要求也越高，如下表所示，可以看一下，硬盘、内存的配置都比较好满足，可能对cpu的要求要高一点，对应着华为的一些产品也有一些，对于操作系统和数据库这一块，也有两个版本，一个是window server2008R2，或者是novell suse linux，

**服务器安装环境介绍：**

| **管理节点** | **最低服务器配置**                           | **推荐配置**                                                 | **操作系统**                                                 | **数据库** |
| ------------ | -------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 0-200        | CPU：1*双核2G以上，内存：4G，硬盘空间：40G   | Huawei：TecalRH2288H V2-1*E5-2630 V2 CPU，2*4GB内存，2*300GB | 配置1：Windows Server 2008 R2标准版（64位）（中文简体或英文版本）/Windows Server 2012 R1标准版（64位）（中文简体或英文版本）+ MySql5.5（标准版网管软件包中自带）/Microsoft SQL Server 2008 R2-标准版配置2：Novell SuSELINUX Enterprise Server-多国语言版本-企业版-11.0 SP3 （中文简体或英文版本）+ Oracle Database Standard Edition 11g R2注：20000管理节点推荐使用配置2。 |            |
| 200-500      | CPU：1*双核2G以上，内存：4G，硬盘空间：60G   |                                                              |                                                              |            |
| 500-2000     | CPU：2*四核2G以上，内存：8G，硬盘空间：120G  | Huawei：TecalRH2288H V2-2*E5-2630 V2 CPU，4*8GB内存，3*300GB |                                                              |            |
| 2000-5000    | CPU：2*四核2G以上，内存：16G，硬盘空间：250G |                                                              |                                                              |            |
| 5000-20000   | CPU：4*四核2G以上，内存：32G，硬盘空间：320G | Huawei：TecalRH2288H V2-2*E5-2630 V2 CPU，4*8GB内存，3*300GB |                                                              |            |

（服务器在装完之后，真正取管理的时候，是通过浏览器去管理的，那么对浏览器的版本也是有要求的，Internet Explorer 9.0/10.0、Mozilla Firefox 27.0/30.0/31.0、Chrome 29/30/31这些浏览器的版本都是可以满足的，分辨率，1027*768这些分辨率根本就不是限制条件了，内存1G以上，也是比较容易满足的。）



客户端安装环境介绍：

浏览器版本： Internet Explorer 9.0/10.0 、 Mozilla Firefox 27.0/30.0/31.0 、 Chrome 29/30/31 。

推荐分辨率： 1024x768 像素。

内存：至少 1G 以上。

客户端安装环境对操作系统没有特殊要求，对浏览器版本以及内存有以上要求。

## **安装规划**

这个eSight作为一个网络管理，在安装之前需要一定的参数配置的，比如这个ip地址，主机名，密码等等，

安装 eSight 系统前，需先规划好安装信息（如 IP 地址、主机名、密码等），以便快速、正确地安装 eSight 系统。

主机名和 IP 地址规划：可以根据实际情况修改服务器的主机名、 IP 地址。

（这个地方需要注意一下，安装完了之后有一个缺省的用户名和密码的，第一次登录的时候要用，所以需要稍微记一下，）

用户名和密码规划：初始默认用户名密码为 admin/Changeme123 ，第一次登录 eSight 系统时，会提示修改密码。

（建议数据库和eSight系统安装，不要跟操作系统安装在一起，缺省就是安装在D盘上的，如果有D盘的话，所以不用改也是可以的，）

磁盘分区规划： C 盘为操作系统， D 盘用于安装数据库和 eSight 系统。

安装路径规划： D:\eSight ，可自行设置。

时区规划：发货到现场后，请根据实际情况修改时区和时间。

eSight 服务器 IP 地址：

必须使用静态 IP 地址。

eSight 支持 IPv4 、 IPv6 及 IPv4 和 IPv6 双栈，请根据实际组网规划。

服务器端与所管设备能正常通信。

服务器端与客户端能正常通信。

##  **软件获取**

（软件获取，如果是购买的话，会通过光盘过来的，也可以通过去华为的网站上去下载，官网上是可以下载的，当然是，需要注册一下用户，注册完用户，直接就可以下载，下载下来之后，是一个试用版，（这个试用版是精简版，标准版，专业版里边的精简版，）只能管60个设备，而且还会有一个时间的限制，在这个时间限制内，可以购买这个license，把license导进去之后，就根据你的license获得相应的权限，）

eSight 有两种安装方式：

通过光盘安装：需要准备相关光盘。

通过软件包安装：需要准备相关软件包。

软件获取方法：

华为企业网网站： http://enterprise.huawei.com/cn/

安装软件：选择“技术支持 > 文档与软件下载 > 企业网络 > 网管与控制器 > 产品分类 > eSight > eSight Network > 软件”下载。



## **安装数据库** 

（在正式安装之前，要安装数据库，eSight支持两个数据库，一个是MySql数据库，这个是开源的，如果不想花钱的话，用这个开源的也是可以的，还有一个就是SQL Server 2008数据库，用这个数据库来存储网络设备的运行参数也是可以的，） 



在 Windows server 2008 R2 环境下，支持如下两种数据库，用户可以根据需要选择安装：

MySql 数据库：将随 eSight 软件一起自动安装，用户无需手工安装 MySQL 数据库。

SQL Server 2008 数据库：安装 eSight 服务器前， SQL Server 2008 数据库需要手工单独安装，请参见 SQL Server 2008 的安装手册完成数据库的安装。



##  **启动****eSight****安装程序**

（安装完数据库之后， 就开始eSight的安装，不管是软件包还是光盘，文件是一样的，都是这些文件，在最外面有一个setup，进入点开，运行之后，直接就出来一个安装界面，首先是选择语言，一般是中文，如果是海外的话，就选择对应的语言就可以了，）

运行setup.bat进入安装过程，第一步选择语言，即决定了安装盘语言和网管语言。

![img](https://img-blog.csdnimg.cn/20200606010733143.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

安装语言一旦选定，后续安装完成后就无法修改，只能进行重装。 

##  **安装参数**

（ 然后安装参数，就是我们这个设备，它的服务器的地址，一般服务器至少有一个网卡，如果有多张网卡，你就可以选择用哪张网卡，通过这个下拉框，看下你到底用哪张网卡，当然如果只有一张的话，就默认用这个了，访问端口，就是浏览器来访问，缺省是8080来访问，web浏览缺省端口是80，https加密的应该是43，那么这个eSight服务缺省是开在8080的，然后是安装路径，缺省是放在D盘上的，可以进行手动的修改，不跟操作系统在一个盘上。）

![img](https://img-blog.csdnimg.cn/20200606010901504.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

IP 地址：当前服务器默认的 IP 地址。如果服务器存在多个 IP 地址，请在下拉列表中选择对外可用的 IP 地址。

端口：默认为 8080 ，如果该端口被占用，可修改成其他端口号。

安装路径： eSight 软件的安装路径，用户可手工修改。

（参数设置完之后，就可以进行安装了。） 

##  **选择安装组件**

（安装下一步之后，会让你选一个安装组件，这个安装组件如下图所示，一共有两个颜色，一个是灰色的，一个是黑色的，灰色的是基本组件，你不能选，这些是必须要安装的，这些黑色的字体可以去勾选，哪些东西你要安装，哪些你不需要的，这些其实是需要license的，没有license的话，你勾选了，权限是非常有限的，能管理的数量是有限的，有license才能正常使用） 

![img](https://img-blog.csdnimg.cn/20200606010957783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

基础功能包下面的组件默认灰化，为安装必选组件。

业务组件下面的组件内容请根据实际情况选择安装。 eSight 组件支持增量安装，即如果某个组件在第一次安装 eSight 时没有选择安装，也可以在第二次安装 eSight 时再继续选择安装。

不同的 License 会包含不同的组件。



## **数据库服务器参数**

（然后安装完下一步之后，会提示你输入数据库服务器的参数，esight相当于是数据库的用户，要从数据库里存数据，从设备上去了数据之后，取了设备的运行状态来了之后，是要放到数据库里的，然后从数据库里也是要取数据的，比如说一些报表之类的历史数据，所以要有数据库的操作权限，用户名密码之类的，都是需要的。 ）

![img](https://img-blog.csdnimg.cn/20200606011050970.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



当“数据库类型”为“MySQL”时，系统会默认输入数据库的用户名为root，密码为“Changeme123”。“root”是MySQL数据库默认用户帐户，即数据库系统管理员，具有数据库的最高权限。

当“数据库类型”为“SQLServer”时，并且第一次安装eSight时，需手工输入用户名为sa，密码为Changme123。“sa”是SQL Server数据库默认用户帐户，即数据库系统管理员，具有数据库的最高权限。

如果是增量安装，密码项为灰化，无需再次输入。

##  **显示安装过程进度**

（往下就是安装了，安装的话，就是显示的进度条， ）

![img](https://img-blog.csdnimg.cn/20200606011646545.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

##  **安装完成**

（最后就是安装完成了。安装完成之后，点击启用，完成就OK了） 

![img](https://img-blog.csdnimg.cn/20200606011724365.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



##  **启动服务**

（如果没有启用的话，就通过点击这个esight控制台，如果桌面上没有这个控制台，就在开始菜单里面， 有一个菜单项esight，然后有一个控制台，你点击这个控制台，然后就出现了如下图所展示的那样的2图，然后就可以启动服务，然后eSight服务就启动了，）

![img](https://img-blog.csdnimg.cn/20200606011812280.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



启动 eSight 服务方式：

双击桌面上的“ eSight 控制台”快捷图标，单击“启动”，开始启动 eSight 服务；

选择“开始 > 所有程序 > eSight > eSight 控制台”，单击“启动”，开始启动 eSight 服务 .

如果需要开机自动启动，即 eSight 服务随操作系统的重启而自动启动，可执行该步骤：在主菜单中单击“设置”，选中“开机自动启动”

##  **IE9****首次登录**

（启动起来之后，就可以用浏览器登录了。浏览器登录的时候，在地址栏里就输入正确的ip地址，然后你指定的端口号，直接回车，就会显示登录的页面，但是你第一次打开的时候，会首先来报告一个证书问题，这个证书问题是这样的，它的最后一次进去的是一个加密的，https，这个https加密的是，需要有证书的，这个证书是需要有权威机构颁发的，个人电脑上一般来说，国际上通用的权威的机构，已经有的证书已经放在那里了，但是这个证书，是华为内部，或者是自颁发的，就是说这个证书不是真正的国际上的权威机构颁发的，所以会报告这个证书无法验证它的真伪，但是这个证书还必须要，所以在这里就选择继续浏览此网站，尽管是不推荐，直接继续浏览，这时候就进去了。） 

地址栏中输入： http:// 服务器 IP 地址 : 端口号（ 8080 ），按“ Enter” 。

如果是第一次登录，页面显示网站安全证书有问题，单击“继续浏览此网站（不推荐）”。

![img](https://img-blog.csdnimg.cn/20200606011946767.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

IE登录：如果是第一次登录，页面提示此连接不受信任，单击“证书错误”；然后单击“查看证书”；最后单击“安装证书”。

##  **安装证书**

（打开这个页面之后，虽然这次接受了，下次打开之后，还是会这样，显示这个证书有问题，那么我们可以在本地把这个证书接受进来，在本地存上，就代表着你接受这个证书，那么下次就不会弹出之前的那个页面了。然后就可以看到整个进入的页面esight，认证的页面，进入页面，） 

![img](https://img-blog.csdnimg.cn/20200606012106911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



##  **登录系统** **-** **输入用户名密码**

（输入第一次进入的用户名密码： admin Changeme123）

![img](https://img-blog.csdnimg.cn/20200606012200966.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

当首次登录 eSight 之后，需要根据系统提示修改密码。同时请妥善保存修改后的密码，如果 admin 用户的密码一旦丢失，就只能通过重装 eSight 恢复缺省密码。

当密码将要超过有效期时， eSight 会提示需在有效期内修改密码。

## **登录成功** 

（第一次进去之后会让你修改用户名和密码，后续也可以自己去修改，进去之后就会显示这样的页面，如下图所示，网址是一个加密的，第一项是网管服务的地址，第二项是一个主菜单，第三项就是网络运行的一些统计报表，那么这个统计报表是可以定制的，可以通过新首页旁边的加号，去增加一些选项，定制加一个页面，有些你想看的你可以加上，不想看的你可以删掉，4是常用信息和按钮，登进来之后的用户名，退出，帮助等一些信息，5是告警指示灯区，总的告警数是6，然后是严重告警，然后是告警程度次一点的，6是新增portlet，可以进行定制，这些是esight的主页面，具体的操作就是在首页后面的监控，资源里面去操作。）

![img](https://img-blog.csdnimg.cn/2020060601231297.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

Portlet是指以列表、曲线图、柱状图等方式展现设备状态、全网状态等，即显示在首页中的各小区域块中。

##  **License****介绍**

（装完，进去之后，我们要把它用起来，需要有一个license，如果没有license的话，下下来之后就是一个精简版，只能管六十个网元，然后管理能力也是有限制的，而且这个试用期只有九十天，那么需要在90天之内，把这个license激活，华为的这个license其实就是一个文件，但是这个文件需要自己去获得。 ）

License 文件包含了用户与华为公司签署的合同信息、安装网管系统所在的服务器信息等，是一种加密过的授权文件。

用户需手动加载到 eSight 网管系统中，激活 eSight 网管系统的使用权限。

eSight 软件在没有 License 文件的情况下，能使用 90 天，超过 90 天，登录后直接转到更新 License 界面，用户不能进入系统。

试用期内， eSight 只能管理 60 个网元， WLAN 、 MPLS VPN 、 SLA 、 IPSEC VPN 、网流、策略服务器用户数的管理能力都是 10 个。

系统启动时，检测 License 文件不存在，自动进入试用期，试用期为 90 天。试用期管理能力如下： 试用期内，安装的所有功能都能使用。

超过 90 天，登录后直接转到更新 License 界面，用户不能进入系统。



## **License****申请步骤**

（怎么去获得呢？一个是合同信息，这个合同信息需要去买，付钱给华为公司之后，华为公司就会把这个合同号给你，然后你安装在哪台服务器上，有一个叫ESN码，就是设备序列号，这个设备序列号，不是设备外面贴的那个码，而是，进入esight之后，你从菜单license那个选项里面，那个里面会生成一串码，就是这个设备在esight里面会有一个标识码，然后你把这个标识码抄下来，这个才是ESN码，然后去申请，申请需要去华为的官网，在这里把合同号和ESN号同时输进去，就会生成一个license文件，）

步骤 1 ：获取合同信息

在华为公司发货 eSight 网管系统时，授权证书需要客户找相应的代理商获取。其中用户在华为授权认证证书中可获取合同号、产品名称、产品型号信息。

步骤 2 ：获取服务器 ESN

ESN （ Equipment serial number ）：设备序列号，是唯一标识设备的字符串，用来保证将 License 授权给指定的设备。

步骤 3 ：申请 License

登录华为企业业务网站申请： http://app.huawei.com/isdp/



##  **合同信息获取**

（在这个合同里面，会有一个合同号，这个就是一张纸，纸的上面会写上合同号，）

获取合同号、产品名称、产品型号信息。

![img](https://img-blog.csdnimg.cn/2020060601312419.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



##  **ESN****号获取**

（然后ESN号的获取，在esight进去之后，到这个license管理，然后，会出现一个获取ESN的页面，然后点击这个获取ESN，然后会生成一个ESN，然后把这个生成的ESN抄下来，如果有多个网卡，还需要绑定好一个网卡，） 

在主菜单中选择“系统 > 系统管理 > License管理”。

![img](https://img-blog.csdnimg.cn/20200606013249924.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)



License 加载成功后，请使用管理员用户登录 eSight 系统。选择“系统 > 系统管理 >License 管理”，查看 License 有效截止日期，并对照申请的 License 检查功能项和资源项是否正确。

eSight 采用 MAC 地址经过加密转换后所生成的字符串作为设备唯一标识 ESN 。

##  **License****激活申请操作步骤** **(1)**

（接下去就是license的激活，流程就是第一步，第二步，第三步往下走就可以了，激活密码是刚才那个合同里面就有的，然后就点下一步，输入ESN） 

进入“License激活 > 密码激活”页面，输入激活码。

![img](https://img-blog.csdnimg.cn/20200606013447627.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

##  **License****激活申请操作步骤** **(2)**

输入待绑定的服务器的ESN。

![img](https://img-blog.csdnimg.cn/20200606013554440.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

确认激活，然后下载License文件。

![img](https://img-blog.csdnimg.cn/20200606013626212.png)

##  **License****加载与管理**

从网站上把这个license下载下来之后，把这个下载下来的文件导入esight里面的license管理里面，导入license文件之后，就会出现这样一个菜单，然后在这个菜单上面，把这个文件导入进去，然后license就激活了。 

在主菜单中选择“系统 > 系统管理 > License管理”。

![img](https://img-blog.csdnimg.cn/20200606013743368.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70) 

## **卸载****eSight**

（卸载eSight就非常简单了，如下图所示，首先需要进入控制台，把服务停止，停止之后去点击这个卸载的菜单项，）

停止服务：选择“开始 > 所有程序 > eSight > eSight 控制台”，在弹出对话框中单击“停止”；

卸载 eSight ：选择“开始 > 所有程序 > eSight > 卸载 eSight ” 。

##  ![img](https://img-blog.csdnimg.cn/20200606013911712.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70) **卸载完成**

（卸载之后，点击完成就行了。卸载完成之后，会问你是否需要重启，你可以当前重启，也可以后续再重启。重启完之后就卸载干净了。） 

![img](https://img-blog.csdnimg.cn/20200606013952560.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

（接下来看一下esight的部署模式，上面的部署模式，esight，的版本有三个，有精简版，标准版，专业版，精简版就是下载下来，试用，那么标准版就是一个单服务器模式，） 

## **单服务器模式**

eSight应用平台是B/S模式，支持多个浏览器同时接入。

（如下图所示，esight application service 和database其实就是一个NMS,网管工作站，下边是网络，网管工作站用SNMP去取得网络数据，然后再网管工作站就有数据了，然后网络人员，就可以通过浏览器，这里的浏览器可以是IE,也可以是firefox火狐，来访问网管工作站，就可以看到上面所说的一些页面。这是单一服务器的部署模式）

![img](https://img-blog.csdnimg.cn/20200606175256580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

## **分级部署模式**

（分级部署模式就是企业，比较庞大，有分部有总部，分部部署一台esight，另外一个分部也部署一台，然后在总部再部署一台，然后从总部管理下一级的，然后下一级再去管理下一级，如果是单一的设备其实是管不了，一个庞大的网络的时候，就可以用这种分级的部署模式，）

eSight 支持分级管理，以满足企业总部监管各地区网络的需求。

在分级部署模式下，上级网管可以把下级网管加入到系统中，并提供打开下级网管界面的链接。当用户点击下级网管链接时，将会弹出一个新的浏览器窗口，在新的浏览器窗口中将打开下级网管的主页。

![img](https://img-blog.csdnimg.cn/20200606014213260.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

## **与****OSS****系统集成**

（另外esight开放了一些接口，这些接口是跟OSS（运维支撑系统）对接，当企业存在一些运维支撑系统的时候，可能会存在一些自动化的操作，最简单的就是某个公司新进了一些员工，这些员工需要开账号，开通网络或者是VPN这些账号，开通的时候，可能这个流程是电子流程，这个流程走完之后，常规是需要网络管理员，在网络设备上去开一些权限，但是有了这个接口之后，OSS可以自动化的下达指令，给网管，网管，就是esight可以去进行一个权限的设置，这个就相当于管理自动化了。）

eSight 应用平台支持同上层 OSS 系统集成，且通过 SNMP 实现网络告警上报，并与 OSS 告警系统进行对接。

与 OSS 系统集成的优势包括：

通过 OSS 系统提升网络管理的能力。

实现网元管理功能、网络管理功能的分离。

满足企业运维机制的需要。



![img](https://img-blog.csdnimg.cn/20200606014329807.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjQ2Mzg3MQ==,size_16,color_FFFFFF,t_70)

运营支撑系统（ OSS ： Operating Support System ）是运行在网管中心工作站上的网络管理软件。网络管理员通过操作 OSS ，向被管理设备发出请求，从而监控和配置网络设备。

 
