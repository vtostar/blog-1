---
title: Shadowsocks 使用教程及技巧
date: 2017-01-26
categories: 2-Skill
tags:
  - software
  - net
  - shadowsocks
  - original
	- tutorial
---

本教程谨献给那些每次用 ss 看片都要跑来问我的朋友们。

## Windows

### 准备工作

Windows 系统上您可以使用 ShadowsocksR 和 Shadowsocks 两种软件，差异不算很大，这里我们统一使用 ShadowsocksR( 以下简称为 SSR )。如果您学会了 ShadowsocksR 的操作，那么 Shadowsocks 您也一定可以无障碍使用了。**注意，写下本文时，SSR 的最新版本是 4.0.3。在下不保证本文将会随着 SSR 的更新而更新。**

在您预备艹墙时，首先您需要获取 SSR 的可执行文件。您可以从 SSR 的 Github 项目地址获取 SSR 的获取方式( 这句话真的没有语病 )。Github 项目地址：

> https://github.com/breakwa11/shadowsocks-rss

完整可用的 SSR 文件应该是一个压缩包，由作者 breakwa11 发布，内含如下文件：

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_1.png)

其中，我们只需要将红框内的三个文件复制到一个新文件夹即可。**注意：`-dotnet2.0` 版本用于 Windws 7 及以下系统使用，`-dotnet4.0` 版本用于 Windows 8 及以上版本使用。**

### pac.txt & gui-config.json

一个完整可用的 SSR，在其同一文件夹内必须包含 `pac.txt` 和 `gui-config.json` 这两个文件。`pac.txt` 规定了 SSR 代理的域名，按照一定规则写入此文件的域名，都将被 SSR 代理。`gui-config.json` 则是我们的节点列表。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_2.png)

**注意，如果您已经有了这两个文件，将其放入 SSR 同一目录下，并仅执行步骤 1 即可。**如果您没有这两个文件，那么请按照以下步骤操作。

1、双击 `ShadowsocksR-dotnet4.0` 打开 SSR，您的任务栏将会多出一个小飞机的图标
2、右键小飞机，选择 `系统代理模式` -> `PAC 模式`

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_3.png)

3、然后选择 `PAC` -> `更新 PAC 为 GFWList`

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_4.png)

4、添加节点。SSR 内置了很多种方式来添加节点。您可以双击打开 SSR，在 GUI 中手动添加，也可以右键 SSR，进行二维码扫描，或者通过 ssr:// 链接导入。目前的大部分 ss 卖家都提供了批量导出 gui-config.json 的功能，您也可以直接替换文件夹中的 gui-config，重启 SSR 即可。

### 选择节点

右键小飞机，在 `服务器` 一项中即可选择自己想要使用的节点。

### 开机自启

如果您想让 SSR 开机自启，请右键小飞机，打开 `选项设置`，勾选 `开机自启`。

### 如果某些网站打不开怎么办？

即使打开了 SSR，您也不一定能访问某些国外网站。这时候您有两种解决方案：

1. 打开 SSR 的全局代理。右键小飞机，选择 `系统代理模式` -> `全局模式`。此时您所有的流量都将通过 SSR，所以您访问国内网站或使用国内软件，其速度将会变慢。这种方式适合您临时访问某个网站时使用。
2. 将您需要访问的域名加入 `pac.txt`。打开 `pac.txt`，在域名列表处新起一行，按照如下格式填入您想要访问的网站的**根域名**。**注意，左右引号、逗号都是英文半角标点符号。**这种方式适合您经常访问某个网站时使用。

  > "[test].com",

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_5.png)


### 如何测试所有节点中的最优路线？

在 SSR 中，有一个 `服务器负载均衡` 的选项，我们可以借助它大致测出当前最优路线。

右键勾选 `服务器负载均衡`，再选择 `服务器` -> `服务器连接统计`。接着我们打开 Fackbook, Twitter 或者 Instagram 等可以流式加载页面的网站，然后一边将滚轮往下滑，一边观察 `服务器连接统计` 界面，根据延迟和最高下载速度决定当前的最优节点。当您决定当前最优节点后，即可关闭 `服务器负载均衡`。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_6.png)

## Android

Android 端我目前使用的仍然是 Shadowsocks，因为我实在是对 SSR 的配色接受不能。当然，您也可以在 ShadowsocksR 的 Github 项目里找到 ShadowsocksR 的 Android 版。

### 获取 apk 文件

您可以通过以下几个方式获取 Shadowsocks 的 apk 文件：

1. Apkpure: <https://apkpure.com/shadowsocks/com.github.shadowsocks>
2. Google Play: <https://play.google.com/store/apps/details?id=com.github.shadowsocks>

### 添加节点

Android 版本添加和更新节点最方便的方式大概是扫描 ss 节点二维码。您打开 Shadowsocks 后，可以点击左上角的 `shadowsocks` 字样进入节点列表，点击右下角的 fab 即可打开添加方式选项。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_7.png)

如果您想从电脑端正在使用的节点添加到手机，可以双击小飞机图标，在列表上选中您想要添加的节点，将 `SSR 链接` **去勾**，然后点击该链接，右侧二维码区域将会出现该节点的二维码，用手机扫描即可。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_8.png)

### 设置

当您通过手动或者扫描二维码的方式添加二维码以后，就可以返回主界面了。在主界面，您需要将 `Route` 一项改为 `Bypass LAN & China`( 中文版是 `路由`，改为 `绕过局域网及中国大陆地址` )。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/SSGuide_9.png)

至此，您就可以点击右上角的小飞机图标开始艹墙啦~

## ios

如果您不想越狱，那么主流的两个选择如下：

- Surge: <https://itunes.apple.com/us/app/surge-web-developer-tool-proxy/id1040100637?mt=8>
- Shadowrocket: <https://itunes.apple.com/cn/app/shadowrocket/id932747118?mt=8>

## Mac OS

略略略。
