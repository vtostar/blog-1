---
title: 我的 css 野路子
data: 2017-07-24
categories: Code
tags:
  - original
  - front-end
  - css
---

最近给我的博客撸了一套主题，编写过程中也是梳理了一番许久不用的 css 知识，正好凑一篇文章出来。本来想给本文起名《我的 css 之道》，但想来自己的那点破烂东西还远不能称道，顶多算是些野路子，遂有题如此。

## Container and Wrapper

现在的网页布局几乎都有一个居中的效果，在 bootstrap 中，这个样式由 `.container` 选择器控制。而在我的野路子里也有这样一个选择器用来表述布局的最外层，专门用于控制页面的缩进。

scss:

``` scss
@media screen and (min-width: $width-break-point) {
  .container {
    padding: 0 3rem;
  }
}

@media screen and (max-width: $width-break-point) {
  .container {
    padding: 0 2rem;
  }
}

.container {
  box-sizing: border-box;
  max-width: $width-max-container;
  margin: 0 auto;
}
```

而 `wrapper` 通常被用于描述一部分样式的外层包裹，比如将 `wrapper` 设为 `display: flex` 用于实现内部元素的 flex 效果。

html:

``` html
<div class="wrapper">
  <div>inner-1</div>
  <div>inner-2</div>
</div>
```

scss:

``` scss
.wrapper {
  display: flex;
  justify-content: space-around;
}
```

## CSS BEM?

CSS 的 BEM 思想是一个伟大的创新，使用特定的写法就可以把 css 变成类似 id 的效果，几乎完全避免了 css 间的样式干扰。但这种写法也经常被人诟病写法太过丑陋，并且一不小心就会写出极长的选择器。

而 sass / less 等 css 预处理器的使用能很大程度上优化 BEM 的实现。我们完全可以使用嵌套语法和 `&` 符号使选择器的编写变得简单。但实际上 BEM 结构对于小型项目来说仍然太过复杂，甚至不值得去使用。在我的博客主题开发过程中，我就深刻感觉到了这一点。因此我再次发挥创新精神，设计了一套似乎是更加简单的思想，目前自我感觉良好。

首先，我们需要将网站整体分块，并作为一个选择器的根选择器，根选择器保持唯一即可，比如 `header`, `.main`, `footer`。从根选择器内部的第一层开始就是布局选择器。比如 `header` 中的标题，就可以直接书写 `title` 而非 `header-title`。当我需要往内层继续嵌套标签时，就无限级的通过 `-` 进行连接即可，而非 BEM 中的 `--` 或 `__`。

这样做的好处是，我们只需要保证根选择器的不同，就可以实现该选择器内部所有 css 的互不干扰，同时 BEM 的写法也使得我们的选择器会变得极其工整易于阅读。

**NOTICE HERE**:

- 如果 `-` 连接符超过两个，就表示你的 html 嵌套已经超过了三层，那么这时你应当考虑布局的合理性
- 如果是以标签选择器作为根选择器，那么在其他使用了该标签的模块仍有可能出现样式干扰，因此我们最好为标签选择器添加 class 或 id
- 在原生的 BEM 思想中，`-` 仅表示两个单词之间的空格，而在我的野路子中，`-` 直接就是选择器和子选择器间的连接符。因此，我使用了 `_` 来表示单词之间的连接

html:

``` html
<header class="page_header">
  <div class="title">
    <span class="title-meta">
      <span class="title-meta-inner">inner</span>
   </span>
  </div>
</header>
```

scss:

``` scss
header.page_header {
  .title {
    &:before {
      content: '';
    }
    &-meta {
      font-size: 1.6rem;
      &-inner {
        color: #eee;
      }
    }
  }
}
```

当我们的页面中的某个部分有多个“块”进行填充时，比如 `.main` 中会有 `.index` 和 `.post_body` 两个部分，那么我们应当在 `.main` 中将子模块的样式引入，这样能进一步降低 css 之间的关联。

html:

``` html
<div class="main">
  <div class="index"></div>
  <div class="post_body"></div>
</div>
```

scss:

``` scss
.main {
  @import "index";
  @import "post_body";
}
```

## Use rem

rem 是一种基于 html 根元素字体大小而定的单位，比起 px 的死板和 em 的过于灵活，rem 无疑是当下前端开发中的最优解。

我使用 rem 也采用了一种当下较为流行的做法，即在 `html` 选择器中声明字体大小为 `62.5%`。这个值是怎么来的呢？

1rem 默认等于 16px，因此我们在使用 rem 的时候，都需要让想要的 px 数值除以 16 才能获得我们想要的 rem 值。这样无疑增加了许多繁琐的工作，总不能撸 css 还得在旁边摆个计算器吧？

而将字体大小默认设置为 62.5% 是因为

> 10 / 16 * 100% = 62.5%

那么此时 1rem 就等于 10px 了。此时我们可以直接将想要的 px 值除以 10，就能得到相应的 rem 值。

``` scss
html {
  font-size: 62.5%;
  body {
    // 设置网页基本字号为 16 px
    font-size: 1.6rem;
  }
}
```

## Use variables

现在的 css 预处理器甚至是原生的 css 都支持变量的使用，因此我们可以定义一些十分有效的变量用于统一页面风格，并且使修改样式的操作变得更加简单。

比如我们可以定义一些常用的字体大小，并在页面中仅使用这些变量。当我们需要对某一部分的字体大小进行修改时，就可以只变动变量，就可以实现页面整体的修改。

``` scss
$size-regular: 1.6rem !default;
$size-small: $size-regular - .2rem !default;
$size-small-x: $size-regular - .4rem !default;
$size-small-xx: $size-regular - .6rem !default;
$size-large: $size-regular + .2rem !default;
$size-large-x: $size-regular + .4rem !default;
$size-large-xx: $size-regular + .6rem !default;
```

## Color Design

> 一个页面中不要使用三种以上的颜色。

这恐怕是设计师必读金句了。而 Google 的一票设计师根据这句话提炼出了“主色”，“辅色”，“点缀色”原则，并将其运用至 Material Design 中，彻底颠覆了人们对安卓 app 傻大黑粗的印象。至今，Material Design 的色彩哲学也一直被奉为设计圈的标杆。

我个人偏爱性冷淡的颜色搭配，钟爱黑白灰三种颜色，点缀色一般使用红色，其中最爱的就是 `#b7472a`。

目前也有许多专门提供配色方案的网站，以下列举两个自认为不错的：

- <http://colorhunt.co/>
- <https://coolors.co/>

## Font Design

Google Fonts 大法好！

我个人来讲，衬线体最爱 `Bellefair`，非衬线体最爱 `Roboto`。

## Summary

如今的前端框架和 ui 组件越来越多，自己动手撸 css 似乎已经成为了一件“浪漫”的事情。前段时间甚至一度有“前端已经不需要掌握 css” 的论调产生。

有理，但不对。

前端页面 8 分在设计，2 分在代码。现成的 ui 组件可能完美符合你的业务需求，但不一定完美符合你的内心需求。css 作为一门设计驱动的语言能最大程度的体现开发者的风格和审美，而使用前端组件库却不一定能体现之。

不会 css 但能出活的前端，和能用 css 出活的前端，还是有不同的。
