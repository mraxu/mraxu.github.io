---
layout: post
title:  Sentinel FAQ 0.1.0
description: "FAQ"
modified: 2018-8-30 15:20:20
tags: [macOS]
post_type: developer
blogid: 201808300002
categories: [Sentinel]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
# Sentinel FAQ整理
## Sentinel 承接阿里巴巴近10年双十一大促流量的核心场景，以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。其提供丰富的应用场景支持、完备的监控能力、易用的拓展点。

> Note: 中文文档请见[此处](https://github.com/alibaba/Sentinel/wiki/%E4%B8%BB%E6%B5%81%E6%A1%86%E6%9E%B6%E7%9A%84%E9%80%82%E9%85%8D#dubbo)。

# 热点问题
## 1、Q:dashboard不展示监控问题如何排查？
dashboard是一个单独启动的控制台，引入sentinel的应用是一个客户端。它们各自有自己的通信端口，dashboard的端口可通过启动参数-Dserver.port=xxxx进行配置,引入Sentinel的应用默认端口是8719。两者都启动之后，Sentinel客户端在首次进入资源时会初始化并给dashboard发送心跳，之后dashboard控制台会通过客户端提供的端口对Sentinel客户端进行访问。基于此，以下事情是需要做的：

#### 1、客户端应该引入两者进行通信的基础jar包
```xml
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-transport-simple-http</artifactId>
    <version>x.y.z</version>
</dependency>
```
#### 2、客户端启动时加入JVM参数：
应用名称：
```xml
-Dproject.name=xxxx
```

客户端访问dashboard的参数：
```xml
-Dcsp.sentinel.dashboard.server=dashboard的IP:dashboard的启动端口
```

客户端提供给dashboard访问或者查看sentinel的运行访问的参数：
```xml
 -Dcsp.sentinel.api.port=xxxx （默认是 8719)
```
**注意**：Sentinel会在客户端首次调用时候进行初始化，开始向控制台发送心跳包。确保客户端有访问量，才能在dashboard上看到监控数据。另外，还是期待大家养成看日志的好习惯,详见[日志](https://github.com/alibaba/Sentinel/wiki/%E6%97%A5%E5%BF%97)

* 控制台推送规则的日志在 ：${user.home}/logs/csp/sentinel-dashboard.log 中，
* 客户端接收规则日志在 ${user.home}/logs/csp/record.log 中

#### 3.常用排查问题列表：
* 1.确认dashboard和客户端均正常工作
* 2.客户端发送心跳包是否正常
* 3.客户端是否正常上报给dashboard信息
* 4.客户端的启动参数配置是否正确
* 5.fastjson和sentinel保持一致目前为1.2.49
* 6.curl IP:port/getRules?type=flow 等命令查看结果
* 7.发传送到客户端的规则格式是否正确，例如确认一下降级规则的表单是否填写完整
* 8.某些不能访问互联网的坏境比如堡垒机可能导致前端文件无法下载也可能导致图出不来，可以浏览器调试查看到

## 2.关于规则存储与datasource的问题？
#### 1.Sentinel目前的规则是存在客户端应用内存中的，重启之后设置的规则消失
#### 2.规则可以从dashboard侧调用客户端暴露的控制接口，也可以从不同的扩展数据源读取
#### 3.关于推送规则的数据流转：在控制台配置完之后 数据推送到客户机，更新到客户机内存
#### 4.关于DataSource的持久化定制：
DataSource的持久化定制可以参考[动态扩展文档](https://github.com/alibaba/Sentinel/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%99%E6%89%A9%E5%B1%95)
#### 5.关于持久化的一些建议，总体来说就是Datasource用来接受规则，如果用来改变规则，则仅对本机生效。
* 1.不建议客户端去修改zk,因为若干个客户端前后修改同一个zk的值，这样复杂度很高。如果客户端要改变规则，则仅对本机生效，比如例如fileDatasource
* 2.zk可以用来获取推送过来的规则，即接受规则。
* 3.对于有配置中心的集群来说，就是配置中心->zk->Sentinel的DataSource，客户端监听到rule更新以后更新策略
* 4.无配置中心的情况下，可以 dashboard->zk->Sentinel的DataSource，即将zk等配置中心的UI集成到dashboard中
* 5.如果需要每台机器自己保存规则：应该是dashboard->Sentinel的DataSource->应用内内存->本机存储
* 6.我们鼓励大家根据自己的需求去自定义Dashboard
* 7.后面我们会把datasource分成readabledatasource和writabledatasourve: Readable datasource，一般是指zk,apollo,nacos这种，规则的推送次序应该是 zk管理/dashbaord -〉zk ->sentinel datasource ->sentinel,而不是从Sentinel datsource ->zk；
另外一种是Writable datasource适合单机这种

-------

### 1、Q:关于配置参数的指定问题？
A:有几种方式：
* 可通过 JVM -D 参数指定。除project.name 之外，其余参数还可通过properties文件指定，路径为 ${home}/logs/csp/${project.name}.properties 详见[启动项配置](https://github.com/alibaba/Sentinel/wiki/%E5%90%AF%E5%8A%A8%E9%85%8D%E7%BD%AE%E9%A1%B9)
* 也可以放在加载比较早的静态代码块中，从配置文件中读取，这里包括project.name

### 2、Q:关于Sentinel的性能？
A:根剧我们以前做过测试，单机25w qps以下基本没啥影响 超过了这个值会有一个比较明显的5%-10%d的下降

### 3、Q:dashboard重启一下应用然后就不出监控了?
A:客户机10秒心跳，另外服务器端只保留1000*60*5这么长时间。如果客户机有请求,稍等一会刷新一下，界面应该会出来

### 4、Q:Sentinel监控数据能保留多久？
A:Sentinel对监控数据的做法是定时落盘在客户端，然后Sentinel提供接口去查询日志文件。所以Sentinel在监控数据上理论上是最少存储1天以上的数据；然而作为dashboard展示，聚合数据的，则只展示聚合几分钟以内的统计数据。
我们鼓励大家改写dashboard来存储拉取的监控信息，包括实时的和历史的,如果你要长期保存数据，可以借鉴dashboard的拉取聚合方式落库。

### 5、Q:Sentinel的集群限流功能？
A:会在我们的RodeMap里面，详见这里[RodeMap](https://github.com/alibaba/Sentinel/wiki/Roadmap)

### 6、Q:Sentinel关于集群熔断？
A:一般用并行的线程数来杜绝这种情况,保证自己不被下游拖死

### 7、Q:0.1.0版本客户端获取更新规则的server端口设置是不是有点问题？不显示设置都是8719
A:0.1.0 版本多个客户端的话需要显式设置端口，否则上报会有问题。0.1.1版本修复了这个问题

### 8、Q:降级规则，除开自动返回还可以配置其他的规则么
A:需要自己catch block exception然后自定义降级之后的处理逻辑

### 9、Q:资源名可以是整个包吗？因为很多服务,规则配置和流量监控的区别是什么 ?
A:整个包不行,建议规则不需要一开始就定的，只要确认你埋好点就行，如果真的要整个包都埋点可以写个通过包名的拦截器规则
* dubbo等是默认埋点的，可以任何时候需要的时候再制定规则
* 我们的建议是：不需要预先把所有的方法都配置好规则，一些重要的方法再配置规则，一个包里所有的方法都配上限流规则，这听起来不大"负责任"
* 流量监控和规则没关系，配不配规则监控上都看得到
-------
### 10、Q:服务端的默认api 8719端口可以修改么？
A:可以通过csp.sentinel.api.port配置项进行指定

### 11、Q:可以对url参数限流吗? 可以对ip做限流吗?
A:url参数限流在下个版本中会有，时间点可以看看roadmap。如果你的参数不多可以用自定义方法

### 12、Q:集群机器数的限制？500个是？怎么横向扩容？
A:因为dashboard是一个示范作用,它的聚合监控的能力非常有限,所以我们说只支持500台机器以下的应用。但是客户端是没有这个限制的
如果想用监控 还有规则推送，有两个建议:
#### 1.规则推送上:用一个靠谱的推送机制 例如zk apollo nacos 这个的适配 我们已经提供
#### 2.监控上:完全可以用多台机器来拉取数据,这个横向扩展不成问题,然后考虑下监控数据落盘
具体可以看[动态规则扩展](https://github.com/alibaba/Sentinel/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%99%E6%89%A9%E5%B1%95)

### 13、Q：同一台机器起相同的端口不报错？      
A:默认8719被占用以后会自动选择下一个端口,直到有端口为止,选择端口时间会比较长,本地如果起多个应用建议自己设端口

### 14、Q:Sentinel控制台有登录功能或者说权限控制吗？否则生产机岂不是任意人都能修改规则了？
A:没有,dashboard不提供登陆的工具,这种需要自己定制

### 15、Q:请问dubbo适配之后，dashboard簇点链路的资源名如何自定义？
A:可以自定义埋点就行了，[参考wiki：](https://github.com/alibaba/Sentinel/wiki/%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8#%E6%8A%9B%E5%87%BA%E5%BC%82%E5%B8%B8%E7%9A%84%E6%96%B9%E5%BC%8F%E5%AE%9A%E4%B9%89%E8%B5%84%E6%BA%90)
无论是自动适配还是手动埋点，控制台都能看到对应的资源名

### 16、Q:使用Sentinel做全局流控、接口流控、接口+角色流控、接口+用户ID流控分别该如何实现？
接口+角色流控实例：VIP客户一分钟调用600次，一天调用10w次；普通客户60/1w次
A:1. 全局流控，其实可以在系统保护里面，通过配置整体入口qps，来达到这个目的
  2. 接口流控，相当于定义一个资源，目前框架支持
  3，4 实际上分两种：
  * 如果你的角色不多，10种一下，那么可以通过规则里面的调用源来实现
  * 如果角色/id很多，并且粒度非常细，可以把用户id作为参数，用这种维度来限流
### 17、Q:1.为什么使用了netty自己做了一些解析http请求的代码，使用目前开源的框架接收不行吗，这样设计的初衷是什么？
A:1.netty-transport和simple-transport这jar包，这两个包的功能目前是一样的，即目前simple-transport基本上可以实现开放的功能了。我们还引入netty-transport这个包是为了日后的扩展。如果没有这个需要，引入simple-transport就可以了
  
### 18、Q:监控页面的族点链路的核心是流控和降级，请问跟踪链路问题发现及跟踪，这块未来有考虑吗？
A: Sentinel主要用于：熔断降级，流量控制，不是很适合分布式的跟踪，即跨机器的跟踪，也不是sentinel的重点。我们不会做这件事情。如果需要，可以参考引入dapper,pinpoint,dapper,maple 很多这样的理论。 
 

### 19、Q:怎么对特定调用端限流?
A:流控应用如果使用了Sentinel Dubbo Adapter，同时Dubbo的消费者也引入了Sentinel Dubbo Adapter（消费侧用于透传dubboApplication这个参数）则填调用者的appName就好,消费端引入adapter就会自动透传,否则需要自己传 appName

### 20、Q:dashboard中资源名称为什么会有重复的？
A:最顶层的是Context名，用于区分不同调用链路

### 21、Q:关于maven仓库、依赖包无法下载的问题？
A:请检查maven的setting.xml配置,默认的、阿里云的库都可以下的下来,有些是公司的库，公司的库不一定有这些jar包

### 22、Q:所有资源默认错误率达到多少自动降级，有特殊需求的资源另外设置,一个个设置管理成本较高
A: 一般来讲，对于不同资源，限流/降级的策略、阈值都是不同的，对于这种全局的，我们可以评估，目前还不支持

### 23、Q:web端的资源目前都是根据uri限流，有没有根据前缀匹配限流？
A:详见：
* 可以自己实现一个UrlCleaner，处理对应的URI（提取前缀之类的操作）。
* 使用UrlCleaner 的话，对应的资源名都会归到clean后的资源
* Sentinel不区分拦截点和展示点，只有资源的概念。
* UrlCleaner 实现URL前缀匹配只是个trick，它会把对应的资源也给归一掉。直接在资源名粒度上实现模式匹配还是有很多顾虑的问题的

### 24、Q:目前信息抓取和uri指的是？ 各个requestcommandhandle是可以扩展的，监控的web这边的信息抓取和uri目前不支持动态扩展？
A:这些目前都是绑定的API，后续可以考虑支持扩展
 
### 25、Q:sentinel的core和阿里内部用的代码是什么关系？
A:sentinel的core和阿里内部用的是同一套，只有功能的摘取

### 26、Q:心跳包是拦截到第一次调用才开始发送的？ 初始化大概多长时间?
A:心跳包是启动客户端后就会发送的，不过初始化会需要一定的时间，不会很长时间的，如果一直没发心跳，record.log 里有相关日志，看看有什么异常。目前初始化逻辑其实就是起客户端的Server然后初始化任务发心跳，没初始化完成是不是不能发送心跳包，Spring 应用可以在bean里面init

### 27、Q:csp.sentinel.flow.cold.factor这个参数是什么意思?  
A:warmup的参数,warmup有阈值和时长，还有一个就是这个参数，一共3个参数，这个代表qps的令牌桶中令牌产生的速度，具体看一下WarmUpController这个类

### 28、Q:规则里面limitApp（流控应用）作用是什么？
A:limitapp主要是针对调用方的流量控制,比如你提供了一个服务，分别会被A,B,C 几种不同的服务调用。你想分别对A,B,C来做限流，即可

### 29、Q:实时运行数据如何查看？
A:实时运行数据 可以通过[查看]( https://github.com/alibaba/Sentinel/wiki/%E5%AE%9E%E6%97%B6%E7%9B%91%E6%8E%A7)里面提到的方法来实时查看
 
### 30、Q:请问limitApp的埋点情况？
A:如下：
* 如果消费方引用了dubbo-adapter，这个其实对dubbo是自动有效的
* 如果是http那么需要从request头里面拿到
* 对于其它的框架 需要自己去埋点，主要是在ContextUtil.enter(),这里把调用者拿到,contextUtil.enter(resourceName, origin)这里的origin就是调用者
* limitApp这个属性除了系统保护其它的都可以用

### 31、Q:refreshfile每隔三秒扫描加载有点耗资源在加载前判断下文件是否修改比较合适？
A:可以！最好这个可以做成配置项，例如我们常说的启动参数，可以放到properties里面

### 32、Q:关于LeapArray中的sampleCount?
A:如下：
* 我们初始化用了两个格子，
* 格子越多越平滑，但是损害越多；格子越少，其实不平滑但是精确。不同场景用不同的大小，例如秒杀这种，格子越少越好；但是如果是长期高流量，格子10比较好
* 在datasource的扩展属性中可以动态调节

### 33、Q:很多开发通过错误码来处理流程，而非通过异常，这种情况特别多见于历史遗留系统。这种写法，导致哨兵不容易拦截到错误，无法触发降级。对于这种情况，有没有什么好的处置方法呀？
A:实际上Sentinel是通过 Trace.trace(e)来统计异常的,可以这样实现：
* 你在接入的时候只要收到错误码就调用这个函数来统计异常，那么error code就一样能够作为异常被统计到。熔断降级也生效了
* 自定一个Default 的fallback handler来统一处理

### 34、Q:限流的冷启动模式中计算 Token 的时候有一个coolDownTokens() 函数，能解释一下吗？
A:这个是冷启动的时候最低的速率比
### 35、Q:请教一下，限流冷启动模式  WarmUpController 中的canPass()函数里有计算 previousQps，这个previousQps 是表示什么意思呢？
A:其实是一个启动过程 每一秒允许通过的qps和上一秒通过的wps算出来的,其实这个算法脱胎guava但又和guava不一样,但是思路是类似的

### 36、Q:测试发现，同一个线程的flow rule有效，异步调用的跨线程控制无效，应该怎么操作呢?
A:目前我们不支持异步,异步要下个版本
### 37、Q:比如说，冷启动这个限流场景，超过的流量就被拒掉了（抛异常）,consumer侧触发重试，根据rr策略，流量调度到另一个机器，是这样的吗？
A:调度这个高级功能还没有,现在只能拒绝或者排队

### 38、Q:不同的slot执行的先后顺序是固定的吗？
A:详见：com.alibaba.csp.sentinel.slots.DefaultSlotsChainBuilder这个类

### 39、Q:Sentinel跟hystrix相比优势是啥？两者都提供了流控降级以及dashboard
A:[Sentinel 与 Hystrix 的对比](https://github.com/alibaba/Sentinel/wiki/Sentinel-%E4%B8%8E-Hystrix-%E7%9A%84%E5%AF%B9%E6%AF%94)

### 40、Q:InitExecutor.doInit();是否需要在初始化时手工调用
A:不需要，sentinel-core包的Env类通过static块调用了；
demo工程中的InitExecutor.doInit();是为了不让进程退出。

### 41、Q:InitExecutor.doInit();已调用，但通过http访问规则失败
A:检查是否缺少sentinel-transport-simple-http依赖，InitExecutor.doInit()中的ServiceLoader.load(InitFunc.class)加载需要。