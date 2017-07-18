---
title: Hexo 双线部署及性能优化
date: 2017-01-30
categories: 2-Skill
tags:
  - hexo
  - net
  - github
  - coding
  - original
	- tutorial
---

本文旨在从两个方面对 Hexo 的访问速度进行优化。

## 为主题设置外链字体库

我使用的主题是 NexT，其字体默认使用 Google Fonts，而 Google Fonts 在国内的访问速度极其蛋疼，这也直接导致大陆地区加载博客极其缓慢。好在 Hexo 给出了自定义字体的选项，我们可以将字体库的引用改为国内 CDN。NexT 字体设置的官方文档：

> http://theme-next.iissnan.com/theme-settings.html#fonts-customization

打开 NexT 主题的设置文件 `_config.yml`，通过搜索找到 `font:` 这一栏，在 `host` 中，填入您找到的国内 CDN。目前我在使用的是下面这个：

> https://fonts.css.network/

此方法适用于其他使用 Google Fonts 的主题。

## Hexo 双线部署

**NOTICE HERE**: 现在 Coding.net 非会员用户创建的 Coding Pages 在访问时时会加入几秒钟的广告，请谨慎考虑是否使用

在我之前写过的“Hexo 不完全指南”一文中，我仅使用了 Github 作为文章部署地址，这将导致国内用户访问我的博客不会特别快。解决方案就是将部署地址改为国内的 Coding，可是这将导致国外用户访问速度变慢。其实，我们可以通过一些简单的设置，实现国内访问 Coding 服务器，国外访问 Github 服务器的效果。

在此之前，我们需要做几个准备工作：

1. 注册 Coding 账号
2. 新建一个名为 `[user_name].coding.me` 的公开仓库，并开启 pages 服务
3. 绑定自定义域名
4. 将 Coding 通过 SSH 密钥的方式与本机连接

上述工作完成后，我们就可以开始下面的设置了。

### 设置部署地址

打开 Hexo 的 `_config.yml` 文件，将 `deploy` 这一栏改为如下代码，格式为 `名称： 仓库,分支`：

```
deploy:
  type: git
  repo:
    github: git@github.com:[user_name]/[user_name].github.io.git,master
    coding: git@git.coding.net:[user_name]/[user_name].coding.me.git,master
```

### 设置域名解析

我的域名目前托管在阿里云，并且可以自由选择 `解析路线`。如果您的域名供应商处没有提供此设置，可以考虑将域名 DNS 改为阿里云的 DNS 服务器。

在解析控制台中，将指向 Github Pages 的解析路线设置为 `海外`，将指向 Coding Pages 的解析路线设置为 `默认`，依次保存即可。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/HexoOptimization.png)

## 一些链接

- NexT 主题官网：<http://theme-next.iissnan.com/>
- 常用前端公共库 CDN 服务：<https://css.net/>
- 极客族公共加速服务：<https://cdn.geekzu.org/>

最后，对所有开源主义者和公益项目提供者表示由衷的感谢。
