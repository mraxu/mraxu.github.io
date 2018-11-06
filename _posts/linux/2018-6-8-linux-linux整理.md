---
layout: post
title:  Linux旧知识整理
description: 整理归纳总结
modified: 2018-6-8 15:20:20
tags: [linux]
post_type: developer
blogid: 201806080001
categories: [linux ]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
# 1.Linux简介「了解」
- 1.1.Linux介绍
  - 是类Unix计算机操作系统的统称
  - 内核名字也是`Linux`
  - 是芬兰大学生Linus Torvalds于`1991年`编写的
  - Linux这个词本身只表示Linux内核,但在实际上人们已经习惯了用Linux来形容整个基于inux内核,并且使用`GNU`工程各种工具和数据库的操作系统

- 1.2.Linux发行版组成
  * Linux内核
  * 应用软件
    * 1.2.1.一些GNU程序库和工具
      * 1.Emacs集成开发环境和文本编辑器
      * 2.GCC语言编辑器
      * GNOME
    * 1.2.2.Shell
    * 1.2.3.图形桌面环境
      * KDE(qt编写)
      * GNOME(GTK编写)
      * Unity
    * 1.2.4.一些办公套件
      * OpenOffice
    * 1.2.5.编译器
      * gcc
      * g++
    * 1.2.6.文本编辑到科学工具的应用软件
      * vi
      * gedit
- 1.3.Linux版本
  * 商业公司维护的发行版本「Redhat」系列
    * RHEL「Redhat Enterprise Linux」也就是所谓的Redhat Advance Server「收费version」
    * Centos「Redhat社区克隆版,免费」
    * FedoraCore「由原来的Rethat桌面版本发展而来,免费」
  * 社区组织维护的发行版本Debian系列
    * Debian
    * Ubuntu
    * 其他发行版可详细查询[distrowatch](http://distrowatch.com/)和[Linux distrowatch Timeline](https://en.wikipedia.org/wiki/File:Linux_Distribution_Timeline.svg)

# 2.Linux目录结构
- 2.1.根目录结构
  - `dev:`设备文件所在目录「device的缩写」
  - `etc:`包含了当前操作系统用户所有配置的相关信息
  - `home:`当前操作系统所安装的用户的主目录
  - `lib:`操作系统使用的库文件以及相关的配置都放在此目录下
  - `mnt`一般为手动挂载的目录
  - `media`一般为系统自动挂载的目录
  - `usr`unix软件资源包管理目录,存放的是当前用户下的一些东西
  - `bin`Linux操作系统下可以执行的系统级的二进制命令「binary简称」
  - `sbin`超级用户需要用到的二进制命令存储在该目录下「super binary简称」
  - `boot`系统在开机的时候需要加载的一些文件和配置
  - `lost+found`存放系统错误产生的文件碎片,方便用户查找和恢复
  - `proc`内核提供的一个接口,主要用来存储系统统计信息
  - `root`root用户的宿主目录

- 2.2.目录路径介绍
  - `绝对路径`:从根目录开始描述的路径,也就是从 "/" 开始
  - `相对路径`
    - 从当前位置开始描述的路径
    - `.`表示当前目录
    - `..`表示当前目录的上一级目录
    - 两个临近目录直接进行切换,命令:`cd -`
- 实例
**xuguojing@xuguojinglinux:~$**
- 1.第一个`xuguojing`:当前登录的用户
- 2.`@`:英文at的意思,表示在
- 3.第二个`xuguojinglinux`:表示主机名「hostname」
- 4.`~`:当前工作目录的位置:宿主目录
- 5.`$`:表示当前登录的用户为普通用户,如果是`#`则为超级用户

# 3.Linux 命令「会出现一些子功能选项」

## `tree`
  - 以树形形式显示当前文件和目录
  - 需要安装该软件:sudo yum -y install tree「centos下」

## `ls`「查看指定目录下所有文件和目录信息」
  - -a「all」 列出当前目录下所有文件内容
  - -R「recursive」 同时列出所有子目录
  - -l 除了文件名之外,还将文件的权限,所有者,文件大小等信息详细列出来

## `cd`「进入指定目录 cd+path」
  - 相对路径--> cd./xuguojing/guojing
  - 绝对路径--> cd /home/xuguojing/guojing
  - `cd ..` 当前目录的上一级
  - `cd .` 当前目录
  - 进入家目录(/home/axu)三种方式:
    - cd
    - cd ~
    - cd /home/axu

## `pwd`「查看当前所在目录 」printf working directory的缩写
- 创建和删除目录
  - 创建:`mkdir + 目录名`
    - mkdir world --> 创建world目录
    - mkdir -p world/a/b --> 创建多级目录加参数`-p`
  - 删除:`rmdir + 目录名`「只能删除空白目录,使用率不高」
- 创建和删除文件
  - 创建:`touch + 文件名`
  - 删除:`rm + 文件名`,`rm -rf + 文件名``为强制删除所有文件/文件夹

## `cp`「拷贝」
  - 拷贝文件
      - cp file1.txt file2.txt 「将file1.txt的内容拷贝到file2.txt中」
        -  文件不存在创建文件
        - 文件存在,覆盖源文件
  - 拷贝目录
    - cp -r dir1 dir2 -->「将目录dir1的内容拷贝到dir2中」
      - dir2目录不存在创建目录
  - `scp`「超级复制」super copy的缩写
    * 使用该命令的前提条件 --> 目标主机已经成功安装`openssh-server`
    * 使用格式:
      * `scp -r` 目标用户名@目标主机ip地址:/目标文件的绝对路径/保存到本机的绝对路径或者(相对路径)
      * 在后续会提示输入「yes」此时,只能输"yes",而不能简单输入「y」
      * `scp -r`目标用户名@目标主机ip地址:/目标文件的绝对路径/保存到本机的绝对/相对路径
      * scp -r usertest@192.168.1.2:/home/usertest/test /home/xuguojing/test

## 3.1 查看文件内容

### `cat`将文件内容一次性输出到终端,如果文件太长,无法在终端全部显示
  - 使用格式
    - cat file1.txt

### `more`文件内容分页显示到终端,但是只能一直向下浏览,不能后退
  - more + 文件名
  - 相关操作
    - 回车:显示`下一行`
    - ctrl+c 或者 q 退出
    - 空格:显示`下一页`

### `less`文件内容分页显示到终端,可以自由浏览
  - 相关操作
    - 回车:显示`下一行`
    - 空格:显示`下一页`
    - ctrl+p 或 ↑:滚动到上一行
    - ctrl+n 或 ↓:滚动到下一行
    - q:退出

### `head`从文件头部开始查看前x行的内容

  - head -5 hello.py --> 查看hello.py文件前5行的内容
  - 如果没有指定行数,默认显示前`10`行内容

### `tail`从文件尾部开始查看后x行的内容
  * tail -5 hello.py --> 查看hello.py文件后5行的你日工
  * 如果没有指定行数,默认显示前`10`行内容

### `ln`
 * 软链接「符号链接」 「相当于windows下的快捷方式」
 * 注意事项
   * 创建软链接:源文件要使用绝对路径
   * 软链接大小:源文件+路径 的总字节数
   * 目录可以创建`软链接`
 * 示例:
   * ln -s /home/xuguojing/guojing/a.txt「源文件+绝对路径」a.txt「软链接的名字」
 * 硬链接
   * 注意事项
     * 以文件副本的形式存在,但不占用实际空间
     * `不允许`给`目录`创建硬链接
     * 硬链接只要在同一个`文件系统`中才能创建
   * 硬链接能够`同步更新`
     * linux下每一个文件都对应一个lnode,创建硬链接后两个文件的lnode是相同的
     * 查看文件中的lnode:stat test.txt
     * 文件创建链接后,硬链接计数+1
     * 删除一个硬链接,硬链接计数-1

## 3.2 文件或目录属性
    * `wc`查看文件的字数,字节数,行数
    * wc a.txt
      * 行数 字数 字节数 文件名
      * 7    23   120   a.txt  「结果显示」
    * 子功能参数
      * -c :只显示字节数
      * -l :只显示行数
      * -w :只显示字数
    * `ad`查看二进制文件信息
    * `du`查看某个目录的大小「disk use的缩写」
    * `df`查看磁盘的使用情况「disk free的缩写」
    * `which`查看指定命令所在的路径
      * which指令会在PATH变量指定的路径中,搜索某个系统命令的位置,并且返回第一个搜索结果

## 3.3 文件权限,用户,用户组相关命令
  * `whoami`查看当前登录用户
  * `chmod`修改文件访问权限「change mod的缩写」
    * 修改方式:
    * 1.文字设定法:
      * chmod [who][+|-|=][mod]文件名
      * 示例:chmod u +wxr axu.py
        * 操作对象[who]
          * `u`表示用户「user」
          * `g`同组用户「group」
          * `o`其他用户「other」
          * `a`所有用户「all」默认
        * 操作符[+|-|=]
          * `+`添加权限
          * `-`取消权限
          * `=`赋予给予权限并取消其他权限
        * 权限[mod]
          * `r`读取
          * `w`写入
          * `x`执行
    * 2.数字设定法:
      * 数字代表的含义:
        * `0`没有权限
        * `1`执行权限「x」
        * `2`写入权限「w」
        * `4`读取权限「r」
      * 示例:chmod 777 file.txt
  * `chown`将指定文件的拥有者改为指定用户或组「change owner的缩写」
    * 用法:
      * chown + 文件所属用户 + 文件或目录名
        * chown xuguojing test.txt
      * chown + 文件所属用户:文件所属组 + 文件或目录名
        * chown guojing:guojing test.txt
  * `chgrp`改变文件或目录的所属群组
    * 用法
      * chgrp + 用户组 + 文件或目录名
      * chgrp guojingzu test.txt

## 3.4 查找和检索

### `find`
* 按文件名查询: `-name`
   * find + 路径 -name + 文件名
   * find /home/axu/ -name a.txt
* 按文件名大小查询`-size`
   * find + 路径 -size + 范围
     * 范围
       * 大于用`+`表示,+100k
       * 小于用`-`表示,-100k
       * 等于`不需要`添加符号 100k
     * 大小
       * `M`必须大写
       * `k`必须小写
       * 示例:
         * 等于100k的文件: `find ~/ -size 100k`
         * 大于100k的文件: `find ~/ -size +100k`
         * 小于100k的文件: `find ~/ -size -100k`
* 按文件类型查询`-type`
  * fine  路径 -type 类型
     * 1.普通类型用`f`表示,而不是`-`
     * 2.目录`d`
     * 3.符号链接`l`
     * 4.块设备文件`b`
     * 5.字符设备文件`c`
     * 6.`s`「socket」,网络套接字
     * 7.管道`p`
     * `例子`:find /home/axu -type d

### `grep`
* 按文件内容查找
  * 参数`-r`
  * grep -r "查找的关键字" + 路径
  * `例子`:grep -r "xuguojing" /home/axu

## 3.5 压缩包管理
