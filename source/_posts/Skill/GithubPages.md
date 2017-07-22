---
title: Github Pages 知识梳理
date: 2016-12-10
categories: 2-Skill
tags:
  - net
  - github
  - original
  - tutorial
---

之前一直被 Github Pages 搞得很迷，昨晚通过自己的实验，总算是有了清晰的思路，故在此梳理一番。

## 到底需不需要 gh-pages 分支？

网上关于 Github Pages 的第三方介绍都比较简单，而且有很多矛盾的描述。你会发现有些人不创建 gh-pages 分支，而有些人则创建了该分支。实际上，Github Pages 是既可以在 master 分支建立，也可以在 gh-pages 分支上建立的。其区别在于，如果你在 master 分支上建立 Github Pages，那么你必须将网页文件统统放在 master 分支下。那么如果你的仓库不是前端项目，或者不打算制作为博客，而是只需要一个不太复杂的项目展示页，那么你就可以通过创建一个 gh-pages 的方式来单独存放网页文件，而 master 分支存放项目内容。

## Github Pages 的分类

根据 [Github Pages 官网](https://pages.github.com/)的解释，Github Pages 分为 `User or organization site` 和 `Project site` 两种形式。这两种形式的区别如下：

### User or organization site

如果要创建这种页面，你需要新建一个名为 `{yourUserName}.github.io` 的仓库，{yourUserName} 就是你的 Github 用户名。比如我的用户名是 varzy，那么我需要创建的仓库名称就是 varzy.github.io。**这个站点相当于入口，也相当于网站的顶级域名，**所以网上很多人用这种方式去制作自己的个人博客或网站。比如我就用了这种方式制作了该博客。如果有兴趣，欢迎参考我的这一篇文章：[Hexo 不完全指南 - 安装、备份、注意事项](http://varzy.me/2-Skill/HexoGuide/)。

使用这种仓库，一般是不需要创建 gh-pages 分支的，我们会直接使用 master 分支来存放网站文件。当然，如果你更想使用 gh-pages 分支来存放网页文件也不是不可以。

### Project site

如果你的某一个仓库需要一个简单的页面来介绍它的相关内容，那么你就可以新建一个名为 gh-pages 的分支，并将网页文件存放于该分支下。Github 将默认将此分支下的内容解析为一个 Github Pages，而不需要进行任何设置。

Project site 的域名规则是 `{yourUserName}.github.io/{repoName}`。比如我有一个名为 demo 的仓库，那么当我创建了 gh-pages 分支并推送后，就可以在浏览器中敲入 varzy.github.io/demo 来访问该项目的 Github Pages。

## 域名绑定

任何一个项目页面都可以绑定自定义域名，只需要将域名使用 CNAME 记录指向自己的 Github Pages 地址，并在 master 分支或 gh-pages 分支下建立名为 CNAME 的文件，将需要绑定的域名写入其中即可。

大致思路如此，具体做法不再赘述。

## 一些自问自答

**Q: 为什么我的 Github Pages 不加载引用资源(css, js, 图片)？**

index.html 必须放置在用作 master 分支或 gh-pages 分支的根目录下，并且 index.html 中的资源引用路径必须正确。

**Q: Github Pages 有没有什么限制？**

有的。详见 Github Pages 帮助文档：

> GitHub Pages source repositories have a recommended limit of 1GB .
> 
> Published GitHub Pages sites may be no larger than 1 GB.
> 
> GitHub Pages sites have a bandwidth limit of 100GB or 100,000 requests per month.
> 
> GitHub Pages sites have a limit of 10 builds per hour.

**Q: 国内 Github 访问缓慢，有没有解决办法？**

共有三种解决方案，请按需选择：
- 去把墙炸了；
- 教会所有看你博客的人翻墙；
- 选择国内的 [Coding.net](https://coding.net/) 来存放你的页面。
