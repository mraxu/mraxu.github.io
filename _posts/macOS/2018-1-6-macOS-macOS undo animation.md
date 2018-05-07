---
layout: post
title:  macOS 关闭动画
description: "用vmware运行macOS 太卡时可以使用"
modified: 2018-1-6 15:20:20
tags: [macOS]
post_type: developer
blogid: 201801060002
categories: [macOS]
image:
  feature: posts_header/abstract-7.jpg
  credit:
  creditlink:
---
# macOS关闭动画
## 1、关闭窗口和对话框弹出的动画特效
 
打开窗口（`Finder-应用程序-实用工具-终端`）并运行下面的命令，就能取消对话框和窗口在屏幕中央位置弹出的效果：
```
defaults write -g NSAutomaticWindowAnimationEnabled -bool FALSE
```
然后`注销并重新登录系统`使更改生效。

如果想恢复这个特效的话，可以打开`终端`窗口并运行下面的命令。同样地，需要注销并重新登录使更改生效：
```
defaults delete -g NSAutomaticWindowAnimationEnabled
```
## 2、关闭快速查看的动画特效
 
当你选中某个文件并敲下`《Space》`键时会弹出快速查看窗口。它显示文件内容的预览画面。你可以在终端窗口里运行下面的命令，停用`“快速查看”`窗口从当前文件位置向外扩张的动画效果（这样做也会同时停用快速查看窗口缩回当前文件位置时的动画效果）：
```
defaults write com.apple.finder QLPanelAnimationDuration -int 0;killall Finder
```
命令运行后立即生效。如果想恢复这个动态效果，请打开`终端`窗口并`运行`以下命令（同理，这个更改也是立即生效）：
```
defaults delete com.apple.finder QLPanelAnimationDuration;killall Finder
```
## 3、关闭Mission Control的动画特效
 
在`终端`窗口里运行下面的命令，可以关闭当用户使用或退出Mission Control功能时所出现的动画缩放效果：
```
defaults write com.apple.dock expose-animation -duration -int 0;killall Dock
```
更改在命令运行后`立即生效`。要注意这样也会关闭在使用“显示桌面”（Show Desktop）特效时，窗口向四周急速分散的动画效果。“显示桌面”特效通常是在触控板上用多个手指同时张开的手势来启用的。

如果想要恢复Mission Control功能的默认动画效果，可以打开终端窗口并运行以下命令：
```
defaults delete com.apple.dock expose-animation -duration;killall Dock
```
## 4、关闭文件保存和打印对话框的动画效果
 
每当保存或打印文件时，程序的标题栏位置会向下滑出对话框。要关闭这一动画效果，可打开终端窗口并运行下面的命令：
```
defaults write -g NSWindowResizeTime -float 0.01
```
你需要`注销后再登录系统`来使更改生效。

如果你希望再次看到这个视觉特效的话，可以运行下面的命令，之后同样要`注销再登录系统`使更改生效：
```
defaults delete -g NSWindowResizeTime
```
## 5、关闭Launchpad界面动画效果
 
更改一个隐藏的设置就可以使`Launchpad`界面立刻出现或消失。打开终端窗口并键入下面两行命令，再按下`《Return》`键就可以了：
```
defaults write com.apple.dock springboard-show-duration -int 0
defaults write com.apple.dock springboard-hide-duration -int 0;killall Dock
```
更改会`立即生效`。如果你要恢复之前的动画效果，可以再次打开终端窗口并运行下面的两行命令：
```
defaults delete com.apple.dock springboard-show-duration
defaults delete com.apple.dock springboard-hide-duration;killall Dock
```
在`Launchpad`界面里的应用程序页面划动时，如果你想`立刻切换`到下一页面而不带动画过渡从而减少页面切换所需的时间，那么可以打开终端窗口并键入下面的命令：
```
defaults write com.apple.dock springboard-page-duration -int 0;killall Dock
```
运行后更改会立即生效。如果需要恢复默认状态，请打开终端窗口并键入以下命令：
```
defaults delete com.apple.dock springboard-page-duration;killall Dock
```
## 6、关闭Dock栏的动画效果
 
Dock栏可以启动`隐藏`功能，以便在它用不到的时候会自动滑出屏幕。这样可以为屏幕腾出一些空间。把鼠标移到Dock栏平常所在的位置的边缘时可以让它重新进入屏幕中。右击Dock栏上的应用程序图标和栈之间的虚线，然后就可以选择是否启动隐藏功能。

如果想让Dock栏在需要用到的时候立刻跳入到屏幕里，而不是滑进屏幕，可以在打开的终端窗口里输入以下命令：
```
defaults write com.apple.dock autohide-time-moidifier -int 0;killall Dock
```
如果想要恢复默认的滑动效果，可以打开终端窗口并运行以下命令：
```
defaults write com.apple.dock autohide-time-moidifier -int 0;killall Dock
```