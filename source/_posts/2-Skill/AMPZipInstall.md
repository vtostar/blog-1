---
title: Apache + MySQL + PHP 压缩版安装
date: 2017-03-29
categories: 2-Skill
tags:
  - original
	- tutorial
  - php
---

## Notice here

- 本人使用的操作系统为 Windows 10；
- 在下的软件安装路径在 d: 下 amp 文件夹，并分别新建了名为 apache, mysql, php 的文件夹来存放解压后的文件。下文中凡是出现路径的地方，还请自行替换为您的安装目录；
- 囿于洒家的能力，本文仅介绍了最基础的安装操作。您在操作过程中出现的各种问题，小子不负任何责任，还望诸位担待则个。

## 起步

新建一个名为 `amp` 的文件夹，并新建三个子文件夹，名为 `apache`, `mysql`, `php`

获取 apache、mysql 和 php 的 zip 格式压缩包，并分别解压相关文件至 amp 各个文件夹中

- apache: <http://www.apachehaus.com/cgi-bin/download.plx>
- mysql: <https://dev.mysql.com/downloads/mysql/>
- php: <http://php.net/downloads.php>

添加环境变量

- apache: D:\amp\apache\bin
- mysql: D:\amp\mysql\bin
- php: D:\amp\php

## 安装 Apache

使用文本编辑器打开 `/conf/httpd.conf`，编辑默认目录

```
Define SRVROOT "d:/amp/apache"
```

使用管理员权限的 cmd 执行以下命令

```
httpd -k install
```

如果执行以上命令无反应，有可能需要将名为 `vcruntime140.dll` 的文件拖入 `C:/Windows/System32` 文件夹下

## 安装 MySQL

使用管理员权限的 cmd 执行以下命令以初始化 data 目录。使用该命令，root 用户的默认密码为空

```
mysqld --initialize-insecure --user=mysql
```

继续执行以下命令以安装 mysql

```
mysqld --install
```

## 配置 MySQL

如果使用 5.7.17 及其以下版本，可以复制一份 mysql 根目录的 `my_default.ini` 并重命名为 `my.ini`

如果使用 5.7.18 及其以上版本，需要手动在 mysql 根目录新建一个 my.ini 文件，在管理员权限的 cmd 中执行以下命令以设置 mysql 的配置文件路径

```
mysqld --default-files="d:/amp/mysql/my.ini"
```

5.7.18 以上版本 (可能) 需要安装运行库：`Microsoft Visual C++ 2013 Redistributable Package (MSVCR120.dll)`。下载地址为

> <https://www.microsoft.com/en-hk/download/details.aspx?id=40784>

设置字符编码 (需要保持 [mysqld] 一项在最下方)。设置完毕后需要重启 cmd 并重新登录方可查看编码的更新。查看整体编码命令：`SHOW VARIABLES LIKE 'character%';`

```
[client]
default-character-set=utf8
[mysql]
default-character-set=utf8
[mysqld]
character-set-server=utf8
```

修改 mysql 的 root 用户密码。登陆 mysql，运行以下指令。`('')` 之间的是新密码

```
SET PASSWORD FOR 'root'@'localhost'=PASSWORD('');
```

## Apache 加载 PHP

创建 php 的配置文件。在 php 目录下找到 php.ini-development，复制一份并重命名为 php.ini

> 注意：由于空格的不兼容性，以下命令不保证复制粘贴后可以正常使用。可以使用 `httpd -t` 命令进行语法检查


加载 php 模块。打开 apache 的配置文件 httpd.conf，在模块部分根据自己的 php 版本插入以下内容

```
LoadModule php5_module "d:/amp/php/php5apache2_4.dll"
LoadModule php7_module "d:/amp/php/php7apache2_4.dll"
```

为 php 模块分配任务。在上面的命令下发插入以上命令

```
AddType application/x-httpd-php .php .html
```

引入 php 的配置文件。在 httpd.conf 中搜索并插入 php.ini 的路径

```
PHPIniDir "d:/amp/php/"
```

修改 php 默认时区。在 php 的配置文件 php.ini 中搜索并修改 `date.timezone` 为 `PRC`。注意，需要去掉语句前的注释符号 (分号)

```
date.timezone = PRC
```

## Apache 加载 vhosts 配置文件

打开 http.conf 文件，搜索并取消注释

```
Include conf/extra/httpd-vhosts.conf
```

## php 链接 mysql

将 php 配置成 mysql 的客户端。在 php.ini 中搜索并设置 `extension=php_mysql.dll`，取消其注释

告知 php 在哪个目录下能找到 php 的扩展文件。在 php.ini 中搜索并设置 php 扩展的绝对路径

```
extension_dir = "d:/amp/php/ext"
```

## 安装 phpMyAdmin

- 解压文件至 `/apache/htdosc` 目录 (或将其解压至其他虚拟目录)
- 更改文件名为 `phpmyadmin`
- 复制 `libraries/config.default` 文件至 `phpmyadmin` 主目录，并更名为 `config.inc`
- 搜索并取消 php.ini 中的 `extension=php_mbstring.dll4.23`
- 设置 config.inc 和 config.sample.inc 中的 `$cfg['blowfish_secret']` 为 32 位以上的字符
- 访问 `localhost/phpmyadmin/index.php`

## 安装 Xdebug

- 下载：<https://xdebug.org/download.php>
- 将文件复制到 `amp/php/ext` 目录下，并改名为 `php_xdebug.dll` (非必需)
- 在 php.ini 中添加以下内容

```
[Xdebug]
zend_extension="D:/amp/php/ext/php_xdebug.dll"
xdebug.auto_trace=1
xdebug.collect_params=1
xdebug.collect_return=1
xdebug.trace_output_dir="D:/amp/_xdebug/trace"
xdebug.profiler_enable=1
xdebug.profiler_output_dir="D:/amp/_xdebug/profiler"
```
