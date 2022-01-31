---
title: 将mate8刷上类原生安卓-OmniRom（更新中）
abbrlink: 45316
date: 2020-05-06 11:34:52
tags:
categories:
password:
copyright:
top:
---

> 本篇教程依赖于`OpenKirin`项目。官网网址[https://openkirin.net/](https://openkirin.net/)

<!--more-->



# 注意事项

## ①

若在初次关机后无法开机，显示数据损坏的话，进入奇兔TWRP，在`高级`菜单中选择`移除data分区强制加密`即可解决问题。***此操作会清除所有数据，因此最好在初次启动系统前完成。***

## ②
如果在解锁后有升级或者重装EMUI的操作，请将手机上锁后重新解锁。具体步骤请看[**华为手机bootloader上锁回锁教程及ADB工具下载——精华帖**](https://club.huawei.com/thread-4948399-1-1.html)

## ③

确保您的手机系统版本为`EMUI 8`，否则这篇教程可能不适合您的手机。

## ④

刷机有风险！请在刷机前做好资料备份的实际准备以及**手机可能变砖**的心理准备。本教程不承担任何因按照本教程刷机却最终变砖、资料丢失的后果！***请做好资料备份！！！***

# 解锁bootloader

这一步没什么好说的，淘宝上有很多解锁的商家。随便选一家就好了，在10~30元左右。请记住他发过来的解锁码。后续步骤可能要用到。

# 刷入OmniRom

确认你的手机已解锁，具体表现为在开机时会显示下图的内容

![](https://xulingran-1301400118.cos.ap-shenzhen-fsi.myqcloud.com/mate8%E6%95%99%E7%A8%8B/1.HEIC)

在`OpenKirin`官网下载刷机包。[传送门](https://openkirin.net/)。**请下载在`EMUI 8-based Builds`标题以下的包。**因为某些原因，若您无法访问网站或下载速度不稳定，请采取某种特殊的上网姿势。笔者下载的包名称为`openkirin_omnirom_pie_20191125_alpha_6.2.img`。若有需要的话，笔者会在以后将其上传至baidu网盘。



![](https://xulingran-1301400118.cos.ap-shenzhen-fsi.myqcloud.com/mate8%E6%95%99%E7%A8%8B/2.jpg)

# 刷入奇兔TWRP

在电脑上安装`奇兔刷机`软件。[官网传送](http://www.7to.cn/)。然后先将手机关机。在长按**音量减键**的情况下插入连接至电脑的数据线，当手机屏幕上出现安卓小机器人以及`FASTBOOT`字样时，打开`奇兔刷机`软件，找到`recorvery`刷入选项。点击刷入即可。刷入完成后，执行以下命令，在出现以下画面时按住**音量+键**4秒即可进入`奇兔TWRP`。

```
fastboot reboot
```

![](https://xulingran-1301400118.cos.ap-shenzhen-fsi.myqcloud.com/mate8%E6%95%99%E7%A8%8B/1.HEIC)