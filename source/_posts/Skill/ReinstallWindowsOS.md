---
title: Windows 重装系统教程精简版
date: 2016-09-17
categories: Skill
tags:
  - computer
  - original
	- tutorial
---

最近我的表妹考上了大学，为了防止世界被破坏，为了维护世界的和平，啊呸，为了防止她被修电脑的奸商坑，所以我决定再次写起这篇重装系统的教程，以备她不时之需。

首先声明以下几点：
- 我是菜鸡，若您发现文中的错误，还望给予斧正。
- 这篇教程只涉及 Windows 10 。之前写过一篇洋洋洒洒上万字的教程，自以为神，然而读者却被 bios 和各种分区格式搞得十分混乱，因此本文只打算介绍 Windows 10 的安装。注意：如果你稍微变通一下，也可以用这个方法完美安装 Windows 8 或 Windows 8.1 。
- 这篇教程不带 win 7 玩。如果带上 win 7 ，那就必然要引入一大堆其他的姿势，怕是又要搞晕一大波人了。
- 这篇教程仅使用 U 盘和 iso 格式的原版系统，无需 PE ，绿色安全无污染。
- 这篇教程力求精简，只讲步骤，不说原理。如有性趣，还请自行谷歌。若文中某些链接无法打开，还请自备科学上网姿势。
- 本篇教程使用的方法比起安装 Ghost 系统略显麻烦，但是！装好后的系统干净到令人发指。
- 如果您的电脑主板未被记忆，那么你应当提前提取你的 OEM Key 以进行之后的系统激活。如果这是一台未安装系统的电脑，或者不能提取 OEM key ，那么安装系统后也可以使用 kms 等方式进行激活，激活后的系统与正版系统使用体验完全一致，但并不算是正版系统，且有可能需要每隔 180 天重复激活一次。这方面还请自行斟酌。
- 按照本教程安装系统时，您的电脑出现的任何意外情况，本人概不负责。

## 〇、需要的硬件

- 一台能联网能下载的电脑（废话）
- 一个容量大于等于 8G 的 U 盘，最好为 usb 3.0 接口

## 一、准备工作

### 1、下载 iso 格式原版系统

你可以在 [msdn, i tell you](http://msdn.itellyou.cn/) 找到各种原版系统：

> <http://msdn.itellyou.cn/>

打开网站后，点击侧边栏 `操作系统` 这一项，选择你想要安装的系统版本。此处我选择了最新发布的 `Windows 10, Version 1607` 这一版。接着选择我们需要的语言版本，像我这种四级都过不去的人还是玩简体中文吧。

再然后，我们需要选择系统的版本和位数。关于系统版本的详细说明可以参考维基百科给出的这一词条：

> <https://zh.wikipedia.org/wiki/Windows_10%E7%89%88%E6%9C%AC%E5%88%97%E8%A1%A8>

当你选择好了系统版本后，就要考虑系统位数了。一般来说，如果你的电脑内存**小于** 4G ，就选择 x86 的系统，如果**大于等于** 4G，就选择 x64 的系统。

此处我选择的是 64 位的 `Multiple Editions` 版本，也就是多版本的意思。这种系统集成了不同的系统版本，根据你使用的密钥进行切换。点开详细信息，你就看到一个 ed2k 链接，复制这个链接到迅雷或其他下载工具中，就可以解析出一个 iso 格式的文件，点击下载即可。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_1.png)

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_2.png)

**Tips：** msdn, i tell you 的维护者 余晓榕 长久以来一直免费为大家收录微软各类系统和软件，坚持至此实属不易。前段时间，作者已开通捐助选项，如果你希望帮助和支持他，请点击网站右上角的 `九年相伴` 这一选项，通过扫描支付宝二维码的方式进行转账。

### 2、格式化 U 盘

将 U 盘插到电脑上，最好也插到电脑的 usb 3.0 接口上。当电脑识别出 U 盘以后，右键 U 盘盘符，进行格式化操作。

**注意：**

- 格式化操作将会清空 U 盘内所有内容，所以请提前转移 U 盘中的重要文件
- 格式化时文件系统一定要选择 FAT32

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_3.png)

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_4.png)

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_5.png)

### 3、将系统文件放入 U 盘中

U 盘格式化完成后，就要将下载好的系统文件转移至 U 盘中。用解压缩软件打开下载好的 iso 格式原版系统，然后解压全部文件至 U 盘中。

此处以 WinRAR 解压 Windows 10 Version 1607 为例：

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_6.png)

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_7.png)

等待解压完成后，弹出并拔掉 U 盘。

## 二、从 U 盘安装系统

### 1、进入系统安装界面

**情况一：你的电脑能够正常开机**

注意：如果你现在的系统还是出厂自带的原版系统且能正常开机，那么请务必先使用 `RWEverything` 等工具提取 OEM key 以用于之后的系统激活，使用方法请自行了解。如果你的系统曾经重装过，或者不愿意使用这种方式进行激活，那么你可能需要用到 kms 激活，效果与正版系统完全一致，但有可能需要每隔 180 天重复激活一次。

将电脑正常开机，再把做好的 U 盘启动盘插入电脑上，依次点击下列按钮进入系统安装界面：

> `开始菜单` -> `设置` -> `更新和安全` -> `恢复` -> `立即重启` -> `使用设备` -> `EFI USB  Device`

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_8.png)

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_9.png)

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_10.png)

**情况二：你的电脑已经不能够正常开机了 / 这是一台新电脑 / 这是一块新硬盘**

如果需要安装系统的电脑已经不能够正常开机了，或者你需要给一台新电脑或新硬盘安装系统，那么你可以通过更改启动项的方式来进入系统安装界面。这种方式下，你需要先进入 Boot ，再从 Boot 中选择 U 盘启动。

由于不同品牌不同型号的电脑进入 Boot 的方法不尽相同，所以此处没法详细说明。不过，现在的电脑一般都默认设置为开机时狂按 `F12` 或 `Fn + F12` 即可进入 Boot ，如果不能进入，则强制关机，以消除 Windows 的快速启动效果。之后再次开机，重试几次。如果还是不成功，那就谷歌一下该型号的电脑如何进入 Boot 吧。

进入 Boot 后，一般来说你会发现有两个 USB 打头的选项，这两个的区别你可以自行了解。这里我们都要选择 `EFI USB Device` 。除此之外，你还可能遇到标注 `UEFI USB Device` 或者只有一个 USB 打头的启动项的情况，这时候尽量选择带 `EFI` 的，如果没有就选择 USB 打头的。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_11.png)

### 2、系统安装步骤详解

选择你需要的语言和时区，一般来说可以直接点击 `下一步`。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_12.jpg)

点击 `现在安装`。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_13.jpg)

如果你有正版密钥，或者可用的 OEM key ，可以直接输入。如果没有，请选择 `我没有产品密钥`。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_14.jpg)

此处请根据你的 OEM key 所在的原系统版本进行选择。一般来说大部分可以使用 OEM Key 的系统都是家庭版。如果你没有 OEM Key，或者这台电脑的激活已经被记录了，那么选择哪个都是可以的。此处我选择 `Windows 10 专业版`。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_15.jpg)

打勾后点击 `下一步`。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_16.jpg)

选择 `自定义` 的安装方式。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_17.jpg)

接着我们就到了磁盘管理界面。此处你可以对你的磁盘进行一系列操作，比如删除、新建、格式化。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_18.jpg)

我的电脑有两块硬盘，分别是位于主硬盘位的 SSD ，也就是下图中显示的 `驱动器 0` ，还有就是位于光驱位的 HDD ，也就是 `驱动器 1` 。如果你的电脑只有一块硬盘，那么一般来说都是 `驱动器 0` 。

按照从上到下的顺序，一般来说分区会是这样的结构：
- 系统恢复分区 （450M）
- EFI 系统分区 （100M）
- MSR 保留分区 （16M）
- 主分区 4 （C 盘）
- 主分区 5 （D 盘）
- ......

此处我想让系统装在 SSD 里，那么我需要格式化 `驱动器 0 ` 中的第一个主分区，也就是 `驱动器 0 分区 4` 。为了防止出现引导问题，我们可以删除第一个主分区及之前的所有分区，并重新新建。完成后我将得到一个容量为 119.2G 的 ` 未分配的空间` 。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_19.jpg)

然后我需要将 ` 未分配的空间` 变为系统可用的分区，那么我需要选中 ` 未分配的空间` ，点击右下角的 `新建`，并输入我想要的大小。此处我选择全部分配，那么我就可以直接点击 `应用` 了。

那如果我想分一个 60G 的分区，该怎么办呢？请拿出计算器，算一下 60 x 1024 = 61440 。但是！如果你输入了 61440 点击了应用，那么你会得到一个 59.9G 的分区，这就很尴尬了。为了避免这种情况的发生，你需要给 61440 多加一些空间。经过我的实践，发现加上 560M 左右就可以得到完整的 60G 了。那么我需要输入的是 60 x 1024 + 560 = 62000 。那如果是 80G 呢？那就是 80 x 1024 + 560 = 82480 。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_20.jpg)

点击 `确定` 。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_21.jpg)

你想让系统装在哪个分区，就选中哪个分区，点击 `下一步`。一般来说都选择第一个主分区，它代表的即是 C 盘。

Tips：
> 如果你想安装双系统，那么只需要选中除过原来有系统的分区并点击 `下一步` 即可。比如分区 4 中有一个系统，那么我此时只需要选择分区 5 ，并点击下一步，即可安装双系统。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_22.jpg)

等待步骤完成。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_23.jpg)

当以上步骤全部完成后，会出现一个 10s 的倒计时，请务必在此期间拔掉 U 盘以防止再次进入系统安装界面。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_24.jpg)

到此，整个系统安装已经全部结束了。如果你已经到了这一步，那么恭喜，你已经战胜了最难的步骤，距离进入桌面仅剩一步之遥！接下来，你的电脑将多次重启，请耐心等待直至看到画面。

### 3、后续设置详解

你最先能够看到的画面就是 `建立连接` 。如果你有微软账户并打算在安装系统过程中直接登陆，那么你可以在此处连接网络。如果你没有微软账户或者打算进入系统后再登陆微软账户，那么你可以直接跳过网络连接。我选择在此处连接网络，并在系统安装过程中直接登陆。

注意：有一部分电脑此处没有 `建立连接` 的选项，这可能是由于你没有连接可用的以太网，而无线网卡又不兼容 Windows 10 自带的网卡驱动，造成无法接收无线信号。无须担心，你可以在进入系统后，安装合适的无线网卡驱动以解决这个问题。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_25.jpg)

直接 `使用快速设置` 即可。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_26.jpg)

按需选择

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_27.jpg)

此处即是微软账户的登陆界面。如果有微软账户，可以在此直接登陆，如果没有，可以选择 `跳过此步骤` 或者 `创建一个`

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_28.jpg)

设置 PIN 。PIN 是一个与设备绑定的短数字密码，如果你不愿意每次开机都输入微软账户密码，那么创建一个 PIN 是很不错的选择。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_29.jpg)

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_30.jpg)

按需选择是否 `启用 Cortana (小娜)`

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_31.jpg)

至此，你已经完成了所有的设置工作，请坐等系统进行最后的准备工作。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_32.jpg)

tada~ 这就是重装后的桌面。干净的只有回收站~

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_33.png)

## 三、装完系统后的工作

### 1、激活系统

打开 `开始菜单` -> `设置` -> `更新和安全` -> `激活` 查看系统激活状态，如果显示已激活，那么恭喜，你可以跳过这一步了。

如果显示未激活，你可以通过购买正版 key 、使用 OEM key 的方式进行激活，如果你都没有，那么还可以使用 kms 进行激活。使用 kms 激活的系统与正版系统完全无异，但有可能需要每隔 180 天重新激活一次。

**我必须强调，使用盗版不可怕，不丢人，但使用盗版不应该抱有优越感，你可以不给微软交钱，但还请抱着一颗对微软的敬仰之心。**

此处我不公开提供 kms 激活软件，如果你不自信自己能找到合适的激活软件，或者懒癌发作，可以在本文最下方找到我的联系方式，向我索要。

### 2、验证账户 （如果登陆了微软账户）

打开 `开始菜单` -> `设置` ->`账户` ，你可以在 `管理我的 Microsoft 账户` 下面找到一个 `验证` 的按钮，点击，按照提示对你的账户进行验证即可。

### 3、更新驱动

一般来说，Windows 10 自带的网卡驱动都是可用的，你可以直接连接 wifi 或网线上网。这时候，你只需要打开 `开始菜单` -> `设置` -> `更新和安全` -> `Windows 更新` -> `检查更新` 即可自行更新系统驱动程序和补丁。

如果你的电脑无法上网，或者出现其他异常，你可以用其他电脑在官网下载适合自己电脑的驱动程序，然后转移到自己的电脑上进行安装。一般来说你都能在电脑的背后找到保修贴纸，你可以使用上面的 S/N 码快速找到驱动程序。下面给出几家常见的 OEM 厂商的官方驱动网站：

- 联想 | Lenovo : <http://support1.lenovo.com.cn/lenovo/wsi/Modules/NewDrive.aspx>
- 华硕 | Asus : <https://www.asus.com/cn/support>
- 戴尔 | Dell : <http://www.dell.com/support/home/cn/zh/19/products/?app=drivers>
- 宏碁 | Acer : <http://www.acer.com/ac/zh/CN/content/drivers>
- 三星 | Samsung : <http://www.samsung.com/cn/support/>
- 惠普 | hp : <http://support.hp.com/cn-zh/drivers>

### 4、设置侧边栏各文件夹的位置(可跳过)

Windows 左侧边默认给出了 `视频`、`图片`、`文档`、`下载`、`音乐`、`桌面` 这六大快捷目录，基本能囊括你能见到的大部分文件类型。很多人也习惯于使用左侧边栏的这些目录存放文件，然而，这些目录的默认地址都在 C 盘，如果你直接使用这些目录可能导致 C 盘的空间愈来愈小，so~ 我们可以更改这些目录的存储位置到其他盘符。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_34.png)

以 `视频` 目录为例，右键视频，选择 `属性` -> `位置` -> `移动` ，然后选择一个合适的盘符，并选择你喜欢的文件夹即可更改位置。更改好后，就可以放心的直接往里面塞东西而不用怕 C 盘空间不足啦。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/ReinstallWindowsOS_35.png)

## 四、尾巴

装系统简直就是 21 世纪的必备技能，无论是从省心还是省钱的角度，你都应该学会这玩意。不过如果你有一个会装系统的男(女)朋友，当我没说。

总有一些人认为会重装系统就是玩电脑的大神了，照这个逻辑，会搬砖的人都能盖个卢浮宫出来么？世界上哪有什么大牛，所谓的大牛只是比小白多了一颗爱折腾的心罢了。
