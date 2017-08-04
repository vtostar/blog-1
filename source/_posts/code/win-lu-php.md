---
title: Windows 下撸 PHP 的最佳实践
date: 2017-07-17
categories: Code
tags:
  - original
  - php
  - tutorial
---

撸 PHP 代码讲究的是一个 ~~说学逗唱~~ 开发环境与运行环境的大一统。而 Windows 平台天生与 PHP 相性不合，怎么在 Windows 下撸 PHP 也算是一门学问。谨以此文献给和我一样买不起 mac，玩不转 Gnome，又离不开 Windows 的 phper。

<!-- more -->

## 为什么不使用 vagrant

现成的 vagrant 是好用，但毕竟不是自己撸出来的东西，不一定对自己的胃口。而且对于个人开发者，相较于再花时间学习 vagrant ，还是直接动手撸一套自己的环境更加简单。

## 大致思路

- 代码写在本地，跑在虚拟机
- Git, npm, composer 等工具全部在 Windows 上使用
- 使用端口转发技术和文件共享技术将虚拟机变成自己的服务器

## 推荐使用的虚拟机和系统

- `VirtualBox`: <https://www.virtualbox.org/>
- `Ubuntu Server`: <https://www.ubuntu.com/download/server>

## 前期准备工作

### 在 VirtualBox 中安装 Ubuntu Server

略

### 设置端口转发

VirtualBox 中的虚拟机默认使用 NAT 模式进行网络连接，此时虚拟机的 ipv4 地址是一个不能被 ping 通的虚拟地址。而我们想要让虚拟机作为我们的服务器，必须保证 Windows 和虚拟机之间的通信。有两种解决方案：

- 使用 VirtualBox 的桥接模式。此模式下虚拟机将使用物理机的真实网卡，相当于一台真实的计算机。此时虚拟机将占用一个真实的局域网 ip 地址
- 使用 NAT 模式下的端口转发。这是由 VirtualBox 提供的一个功能，可以将本机的 ip 地址通过监听自定义端口的方式转发至虚拟机，实现通信

由于桥接模式下虚拟机的 ip 会随着真实机的 ip 地址更改而改变，尤其是当我们的物理机经常更换工作地点的时候，那你每次 ssh 连接几乎都要查看新的 ip 地址 (当然也可以选择固定 ip，但每次只能固定某一个 ip 网段的)。但端口转发就仅需一次配置，此后就非常省心了。本文强烈推荐采用端口转发模式。

使用方法：

![WinLuPHP_1](http://oi0t0q67c.bkt.clouddn.com/blog_skill/WinLuPHP_1.png)

### 使用 ssh 连接虚拟机

Ubuntu Server 系统自带了 openssl 软件，因此可以直接使用 ssh。如果你使用了其他系统，可能需要先安装 openssl。

选一款你喜欢的 ssh 连接软件，如 putty，连接你的虚拟机。`Host Name` 为 `localhost`，端口设置为端口转发中自己填写的端口。比如按照我的设置，此处就是 2222。

### 换源！换源！换源！

首先吼一句，**fuck gfw**。然后进入正题。

此处推荐使用清华大学的 Ubuntu 镜像。吃水不忘挖井人，在此对清华大学开源软件镜像站表示由衷的感谢。网站地址：

> <https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/>

首先备份原始的源文件：

``` shell
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

再修改 `sources.list` 文件中的内容为清华大学给定的源。

更新本地源列表：

``` shell
sudo apt update
```

(可选) 更新软件：

``` shell
sudo apt upgrade
```

## 搭建 lnmp 环境

### 安装 nginx

``` shell
sudo apt install nginx
```

### 安装 mysql

``` shell
sudo apt install mysql-server
```

安装过程中需要设置 mysql 的 root 用户的初始密码

### 将 mysql 的默认编码设置为 utf-8

编辑 mysql 的配置文件：

``` shell
sudo vim /etc/mysql/conf.d/mysql.cnf
```

插入字符编码的相关设置：

``` shell
[client]
default-character-set=utf8

[mysqld]
character-set-server=utf8

[mysql]
default-character-set=utf8
```

启动 mysql 服务:

``` shell
sudo service mysql start
```

登录 mysql，用以下命令查看当前字符编码：

``` shell
SHOW VARIABLES LIKE 'character%';
```

如果除了 `character_set_filesystem` 为 `binary`，其余都为 `utf8`，即表示设置成功。

### 使 mysql 的端口转发可用

mysql 的配置中默认禁止来自 `127.0.0.1` 的连接，因此我们修改 mysql 的配置使端口转发可用。

编辑 mysqld.cnf:

``` shell
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```

搜索并注释 `bind-address = 127.0.0.1`

### 安装 php 及其必要扩展

``` shell
sudo apt install php7.0 php7.0-mysql php7.0-fpm php7.0-dev php7.0-mbstring
```

### 启动服务

``` shell
service nginx start
service mysql start
service php7.0-fpm start
```

### 检验劳动成果

在 windows 的浏览器中输入 `localhost:8008`，如果出现 `Welcome to nginx!`，则表示上述步骤完全没有问题。

## lnmp 的一些配置

### nmp 杂七杂八的路径

配置文件路径：

- `nginx`: `/etc/nginx/`
- `mysql`: `/etc/mysql/conf.d/my.cnf`
- `php`: `/etc/php/7.0/fpm/php.ini`

nginx 的默认站点: `/var/www/html`

### 如何设置 nginx 的虚拟主机？

在 `/etc/nginx/` 目录下有 `sites-available` 和 `sites-enabled` 两个目录。其中 `sites-available` 表示可用的主机配置文件，`sites-enabled` 表示启用的主机配置文件。

当需要创建虚拟主机时，我们可以在 `sites-available` 目录下设置 nginx 的虚拟主机配置文件，在 `sites-enabled` 中创建一个软链接指向 `sites-available` 中的配置文件。

## 设置 VirtualBox 的共享文件夹

我们可以将本地的代码文件夹与虚拟机进行共享，那么我们在本地所有的修改就相当于通过 ftp 实时传输到了服务器上，保证我们看到的效果即时线上效果。

### 安装 VirtualBox 的扩展程序

点击 VirtualBox 的 `Devices` -> `Insert Guest Additions CD image` 选项，VirtualBox 将下载一个增强文件并自动插入 cd 介质。接着我们需要在虚拟机上挂载并安装 VirtualBox 的增强文件。

``` shell
sudo mount /dev/cdrom /media
cd /media
sudo ./VBoxLinuxAdditions.run
```

等待安装完成后，取消挂载并弹出介质

``` shell
sudo umount /media
eject
```

重启 Ubuntu 系统

``` shell
sudo reboot
```

### 设置 Windows 上的共享文件夹

在 VirtualBox 的共享文件夹选项中关联一个本地的 Windows 文件夹。步骤略。

### 将共享文件夹挂载至虚拟机上

运行以下指令

``` shell
sudo mount -t vboxsf CodeHub /mnt/cdhb
```

其中，`CodeHub` 是指上一步在 VirtualBox 中设置的共享文件夹名，`/mnt/cdhb` 是虚拟机上的挂载路径。注意：`/mnt/cdhb` 文件夹必须事先手动创建

## 总结

至此，属于你个人的 PHP 开发环境就搭建完毕了。开心的吃个黄焖鸡吧！
