---
title: Hexo 不完全指北
date: 2016-12-08
categories: Skill
tags:
  - hexo
  - net
  - github
  - coding
  - original
	- tutorial
---

## 前言

之前决定迁移博客平台的时候选择了 jekyll，但在下愚笨，连 jekyll 的开发环境都没搭建成功，调整时只能先 push 到 github 才能看到效果，实属痛苦。今日花了一天时间，终于把博客迁移到了 Hexo，顿时有一种脱离苦海的感觉。虽说 Hexo 非常简单，但官方文档实在简略，第三方教程又繁杂不一，我在实践过程中还是遇到了不少问题，因此还是决定自己动手写上一写，一来帮助自己梳理思路，二来如果能帮到遇到相同问题的朋友就再好不过了。如有纰漏，欢迎斧正。

**注意：**

1. 我使用的开发环境为 Windows 10，工具为 Visual Studio Code，博客托管于 Github，图床为七牛云；
2. 我不会把所有的步骤全部列出，而是仅列出我认为必要的部分。如果你有不懂的地方，还请自行谷歌。

## 大致思路

### 关于托管

使用 Github Pages 托管 Hexo。如果你想要提高博客的访问速度，可以将你的 Hexo 部署在国内的 [Coding](https://coding.net/)。

### 关于备份

和 jekyll 不同，Hexo 的博客文件都需要在本地生成，再 push 到远程仓库的某一个分支，所以博客的源文件是无法直接同步至 github 的，活脱脱一个本地文件，几乎零容灾。

这时候我们只能“曲线救国”了。本来我打算使用同步型云盘直接备份整个文件夹，但这样实在既不优雅也不省心。偶然间在知乎看到了一位昵称为“CrazyMilk”的答主给出的方案([点我查看原文链接](https://www.zhihu.com/question/21193762/answer/79109280))，其思路是使用同一个仓库下的两个分支进行管理。主分支保存 Hexo 生成的博客文件，另一个分支保存 Hexo 文件夹的源文件。这种思路非常好，所以我也采用了这种方式进行管理。由于作者给出的回答较为简略，我将在下面的流程中详细演示。

### 关于图床的选择和使用

国内像样的图床确实不多，其中最优解大概就是七牛了吧。但七牛的存储管理实在蛋疼，于是也是使用了一个曲线救国的方案：通过一个名为 `qiniu upload files` 的 chrome 插件对图片进行批量管理，目前感觉良好。 

## 安装并配置 Node.js 和 Git

接下来就要搞 Hexo 了。在使用 Hexo 之前，请先安装 Node.js 和 Git。官网地址：
- Hexo : <https://nodejs.org/>
- Git : <https://git-scm.com/>

**注意：**

1. 最好在科学上网的环境下访问网站并下载文件；
2. 安装 Node.js 时，最好勾选将路径添加至环境变量的选项，可以省去后续自己添加的麻烦。

安装完成后，在 Git Bash 或 cmd 中配置用户名和邮箱，并生成 ssh 密钥。登陆 Github 或 Coding，使用公钥将计算机与远程仓库关联。

## 安装并配置 Hexo

### 安装 Hexo

在命令行中输入以下命令以安装 hexo-cli：

> npm install hexo-cli -g

### 初始化一个 Hexo 目录

等待安装完成后，在你认为合适的目录下创建一个新文件夹作为 Hexo 的根目录，在这个文件夹的空白处按住 `Shift` + `鼠标右键` ，点击 `在此处打开命令窗口`，输入以下命令以初始化一个 Hexo 目录：

> hexo init

等待初始化完成后，输入以下命令以安装依赖包：

> npm install

### 验证 Hexo 是否安装成功

在命令行中，输入以下命令以生成静态网站：

> hexo g

完成后继续输入以下命令以本地运行：

> hexo s

如果命令提示符反馈：`INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.` ，那么请在浏览器地址栏中输入：

> localhost:4000

如果出现以下页面，那么恭喜，你的 Hexo 已经成功部署到本地了！之后如果你需要调试你的博客内容，可以优先使用这种本地查看的方式。

**注意：**在浏览器查看该页面时，必须保证命令提示符为打开状态。如果关闭命令提示符或者键入 `Ctrl` + `C` 停止服务，你的页面将变成空白页。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/HexoGuide_1.png)

## 将本地的 Hexo 博客推送至 Github Pages

### 配置一个合适的 Github 仓库

**注意：** 此步骤所以操作均在 Github 上进行，不需要将此仓库同步至本地。

新建一个用于存放 Hexo 的 Github 仓库，仓库名为 `{yourUserName}.github.io` 。比如，我的 github 用户名是 `varzy` ，那么我的仓库名应该是 `varzy.github.io`。

然后，重点来了。**你的 master 分支将会用于存放 Hexo 在本地生成的网页文件，所以你需要新建一个新的分支并将其设为默认分支，该分支用于存放你的 Hexo 源文件，也就是将此分支用于备份。**比如，我创建了一个名为 `hexo` 的分支，并将其设置为默认分支：

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/HexoGuide_2.png)

打开该仓库的 `Settings`，将页面下拉至 `GitHub Pages` 位置，在 `Source` 中选择 `master branch` 并点击 `Save` 保存。如果不出意外，你将得到一个页面链接：`https://yourUserName.github.io`，这就是你之后将要访问的博客链接。

至此，Github 仓库部分的配置已经全部完成了。可能有小伙伴有疑问，是否可以先将该仓库全部配置好，再 clone 至本地，然后在该仓库的本地文件夹下初始化一个 Hexo 目录呢？经过我的尝试发现这是不行的。`hexo init` 命名将会清空该文件夹下的所有文件，包括 `.git` 隐藏目录，导致与远程仓库的链接断开。所以，老老实实用我现在的步骤进行操作吧~

### 配置本地 Hexo 文件夹

打开本地 Hexo 文件夹，使用 Visual Studio Code 等工具打开 `_config.yml`，在最下方找到 `# Deployment`，将其修改为如下格式：

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:{UserName}/{UserName}.github.io.git
  branch: master
```

保存并关闭 `_config.yml` 文件，在根目录空白处按下 `Shift` + `鼠标右键`，打开命令提示符，输入以下命令以安装 git 依赖文件：

> npm install hexo-deployer-git --save

**注意：**该命令仅适用于使用 git 方式进行部署的情况，如果你采用其他方式进行部署，还请自行查询相关命令。


### 推送本地 Hexo 文件至 Github Pages

在命令提示符中输入以下命令以生成最新的网页文件并推送至远程仓库的 master 分支：

> hexo g -d

### 查看 Github Pages

等待推送完成，你就可以在浏览器中访问你之前得到的 Github Pages 链接了，其格式应为：`https://yourUserName.github.io/`。

如果可以正常访问，那么恭喜，你的博客已经全部完成且可以正常使用了！不过不要慌着去写文章，接下来的微调和后续工作也是非常必要的。

## 备份 Hexo 源文件

### 连接 github 仓库并推送 Hexo 源文件

这一步我将使用命令行的方式说明，当然你也可以用其他的 git 管理工具完成这一步，比如 VSCode 等。

在 Hexo 的根目录下打开 Git Bash 或者 cmd，输入以下命令以初始化一个 git 仓库：

> git init

使用以下命令创建并切换至 `hexo` 分支：

> git checkout -b hexo

添加所有文件到暂存区：

> git add .

提交暂存区所有文件：

> git commit -m "{message}"

通过 HTTPS 方式或者 SSH 方式连接远程仓库，推荐使用 SSH 方式：

> git remote add origin git@github.com:{UserName}/{UserName}.github.io.git

推送 Hexo 目录下的文件至远程仓库的 `hexo` 分支：

> git push -u origin hexo

至此，所有的备份工作就结束了。当你想要更新博客的时候，需要通过 `hexo g -d` 命令发布一次，这时，你更新过的内容会出现在 Github 仓库的 master 分支上，并且自动更新在 Github Pages 页面上，当你访问 UserName.github.io 就可以看到你刚刚更新的内容了。

但是 `hexo g -d` 只更新了远程仓库的 `master` 分支，你还需要通过再次推送源文件至 `hexo` 分支进行源文件的备份。所以，如果你想要更新博客内容，一般的流程是这样的：`本地调试` -> `hexo g -d` -> `git push origin hexo`。

### 通过备份快速生成 Hexo 目录

如果你更换了电脑，或者更换了硬盘，或者巴拉巴拉，总之就是你需要快速得到一份可以写博客的 Hexo 文件目录，操作也非常简单。

当然，你需要先安装 Node.js 和 Git，此过程于之前相同，在此不再赘述。

接着，输入以下命令以安装 Hexo 到本机：

> npm install hexo-cli -g

然后你需要将整个 Github 仓库 clone 到本地：

> git clone git@github.com:{UserName}/{UserName}.github.io.git --depth 1

由于博客这种东西一般不需要回退或查看以前的提交版本，所以这里加入 `--depth 1` 表示只克隆最近一次的提交。这样可以加快 clone 速度，减小文件夹体积。

在该仓库文件夹空白处按住 `Shift` + `鼠标右键` 打开命令提示符，输入以下命令以安装所有的依赖文件：

> npm install

至此，本地 Hexo 文件应该已经可以正常使用了。可以通过在命令窗口输入 `hexo g` 以查看能否正常部署，如果一切正常，那么恭喜，你的 Hexo 文件已经和上一次备份时完全一致了，enjoy it!

## 绑定自己的域名

Github Pages 可以绑定自己的域名，这也就意味着你可以使用自己的域名去访问你的 Hexo 博客。在此不再赘述域名的申请和操作等步骤。

### 搞定域名解析

在下愚笨，找了半天愣是没找到 Github Pages 给出的最新主机 IP，于是我就直接使用 CNAME 记录指向了我的 Github Pages 地址。事实证明这种方式是可行的。操作如下：

打开域名解析设置，添加两个 CNAME 记录，并分别添加 www 和裸域两种记录。这样做的目的是为了使带 www 的域名和不带 www 的域名都能正确进入博客。

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/HexoGuide_3_new.png)

### 添加 CNAME 文件到 Hexo 目录下的 source 文件夹

在 Hexo 目录下的 source 文件夹下新建一个名为 `CNAME` 的文件，里面填写你想要绑定的域名。如果你想要绑定裸域，则只需要填写域名即可；如果想要加入 www 前缀，那么你需要填入 www.yourDomain。比如，我不喜欢加入 www 前缀，那么我的 CNAME 文件只需要写入：

![](http://oi0t0q67c.bkt.clouddn.com/blog_skill/HexoGuide_4_new.png)

**注意：**一定要将 CNAME 文件置于 source 文件夹下而不是 Hexo 根目录，否则你的域名将不能绑定成功。

### 完成文件提交和 Github 方面的域名绑定

分别使用 `hexo g -d` 和 `git push origin hexo` 命令提交两个分支的文件。然后在 Github 中打开该远程仓库，点击 `Settings`，下拉至 `Github Pages` 选项卡，在 `Custom domain` 中填入你需要绑定的域名，然后点击 `Save` 保存。

至此，你的域名绑定就结束了，通过访问你的域名查看是否绑定成功吧。

## 使用七牛云作为图床

由于我的 Hexo 完全托管在 Github，那么如果我把所有的图片都放置在 Hexo 目录中，势必会引起文件夹体积的巨增，以及 push 时缓慢的速度。因此，图床是十分必要的。七牛作为老牌的云服务商，质量还是算是经得起考验的。同样，此处不再赘述七牛云的注册等步骤。

不得不说七牛的文件管理实在不甚好用，好在有朋友开发了不少第三方工具以供选择。而我选择的方案是一款叫做 `qiniu upload files` 的 chrome 插件。安装此插件后，使用七牛给出的密钥即可与之链接。该插件使用了类 Windows 文件夹的操作方式，使用起来比原版的不知道要高到哪里去了。

此处给出 `qiniu upload files` 插件的应用商店链接：
<https://chrome.google.com/webstore/detail/qiniu-upload-files/emmfkgdgapbjphdolealbojmcmnphdcc>

如果有不能科学上网的朋友，或者不愿意使用 chrome 插件的朋友，可以使用一款叫做 `MPic` 的桌面版软件。官网链接：
<http://mpic.lzhaofu.cn/>

## 性能优化

请查看在下的另一篇文章：**Hexo 双线部署及性能优化**

## 尾巴

### 一些注解

- `hexo g` == `hexo generate`
- `hexo s` == `hexo server`
- `hexo d` == `hexo deploy`
- `hexo n` == `hexo new`
- `hexo g -d` == `hexo generate` -> `hexo deploy`
- `npm install` == `npm i`

### 一些链接

- Hexo 官方网站 : <https://hexo.io/zh-cn/>
- Hexo 官方文档 : <https://hexo.io/zh-cn/docs/>
- NexT 主题官网 : <http://theme-next.iissnan.com/>
- Visual Studio Code : <https://code.visualstudio.com/>
- 七牛云官网 : <https://www.qiniu.com/>
- CrazyMilk 给出的方案源地址(知乎) : <https://www.zhihu.com/question/21193762/answer/79109280>

### 一些细节

- 可以通过给 git 添加代理的方式加速 clone, push 等操作的速度
- 如果想要将某些来自 Github 的主题 clone 至 themes 文件夹下，那么你将不能将这个文件夹直接 push 到 hexo 分支。解决方案是删除该主题文件夹下的 `.git` 隐藏文件夹
- 不要在 Hexo 根目录下添加 `.editorconfig` 文件，没什么卵用，还有可能导致 markdown 格式错乱
- 文章标题不能含有 “[]”，也就是中括号，它将导致你的页面生成失败
