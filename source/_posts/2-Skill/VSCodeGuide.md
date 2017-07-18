---
title: VSCode 插件梳理
date: 2017-04-10
categories: 2-Skill
tags:
  - original
	- tutorial
  - software
  - microsoft
---

我的 VSCode 配置，不定时更新。

## EXTENSIONS

- `Auto Rename Tag`: 改变一对标签的其中一个，另一个会跟着改变
- `Beautify css/sass/scss/less`: 目前的 vscode 自带了格式化 html 和 js 的功能，唯独少了 css，故装之
- `Better Merge`: merge 操作出现冲突时，可以在冲突区域通过简单的点击快速解决冲突
- `CSS Peek`: 在 html 中编辑 class 中的 css 代码，也可以快速跳转至相应样式名所在的位置
- `EditorConfig for VS Code`: 为当前项目添加 .editorconfig
- `Git Blame`: 在状态栏显示当前行代码的提交信息
- `Git History`: 查看 git log，美观且强大
- `gitignore`: 为当前项目添加 .gitignore
- `Indenticator`: 高亮当前行的缩进线
- `IntelliSense for CSS class name`: 在书写 html 代码时自动补全已有的 css 名。不过我一般都用 emmet 语法写标签了，不太能用得着这玩意
- `Path Intellisense`: 自动补全文件路径
- `phpfmt`: 格式化 php 代码，不需要自行下载 php-cs-fixer
- `Rainbow Brackets`: 彩色显示括号，便于区分括号归属
- `Settings Sync`: 将插件和配置同步至 Gist
- `snippet-creator`: 快速创建代码片段
- `View In Browser`: 通过快捷键在默认浏览器中打开 html 文件
- `vscode-icons`: 侧边栏文件图标
- `WakaTime`: 统计代码书写情况

## THEMES

- `Monokai Dimmed`: 默认插件之一。js 配色美到不行，是我使用时间最长的主题
- `Railgun Theme`: 目前在使用的主力主题，含有三个 scheme
- `Darktooth Theme`: 配色偏暗，喜欢复古风格的朋友可以试试
- `Material Theme`: VSCode 主题中下载量最高的一个，整体素质不错，但个人认为其配色太过鲜艳，不适合 coding

## SETTINGS

```
/**
* @file   VSCode Main Settings
* @author zy(i@zyis.me)
* @date   last update in 2017.05.03
*/
/**
  * ===================================
  * Editor
  * ===================================
  */
"editor.fontFamily": "'Source Code Pro', 'Consolas', 'Courier New', 'monospace'",
"editor.fontWeight": "normal",
"editor.fontSize": 14,
"editor.lineHeight": 16,
"editor.lineNumbers": "on",
"editor.tabSize": 2,
"editor.minimap.enabled": true,
"editor.wordWrap": "on",
"editor.quickSuggestions": {
  "other": true,
  "comments": false,
  "strings": false
},
"editor.formatOnType": true,
"editor.formatOnPaste": true,
"editor.cursorBlinking": "phase",
"editor.cursorStyle": "underline",
"editor.mouseWheelZoom": false,
"editor.fontLigatures": true,
"editor.renderWhitespace": "boundary",
"editor.renderIndentGuides": true,
"editor.renderLineHighlight": "gutter",
"editor.dragAndDrop": true,
"editor.formatOnSave": false,
/**
  * ===================================
  * Workbench
  * ===================================
  */
"workbench.welcome.enabled": true,
"workbench.colorTheme": "Railgun",
"workbench.iconTheme": "vscode-icons",
// ! Notes
// Leftest: "activityBarBackground"
// Source tree: "sideBarBackground"
// Main Body: "editorBackground"
// Cursor: "editorCursor"
// ! end Notes
"workbench.experimental.colorCustomizations": {
  "editorCursor": "#b7472a",
  "statusBarBackground": "#121212",
  "editorBackground": "#1d1d1d"
},
/**
  * ===================================
  * Windows
  * ===================================
  */
// "window.zoomLevel": -0.2,
"window.title": "${dirty}${activeEditorShort}${separator}${rootName}${separator} - VSCode",
"window.newWindowDimensions": "inherit",
"window.menuBarVisibility": "toggle",
/**
  * ===================================
  * File Explorer
  * ===================================
  */
"files.insertFinalNewline": false,
"files.autoSave": "onFocusChange",
"explorer.openEditors.visible": 5,
/**
  * ===================================
  * HTTP
  * ===================================
  */
"http.proxy": "http://127.0.0.1:1080",
"http.proxyStrictSSL": false,
/**
  * ===================================
  * Markdown
  * ===================================
  */
"markdown.styles": [],
/**
  * ===================================
  * PHP
  * ===================================
  */
"php.validate.executablePath": "d:/amp/php/php.exe",
/**
  * ===================================
  * Integrated Terminal
  * ===================================
  */
"terminal.integrated.shell.windows": "C:/Windows/Sysnative/WindowsPowerShell/v1.0/powershell.exe",
/**
  * ===================================
  * Beautify css/sass/scss/less
  * ===================================
  */
"beautify.tabSize": 2,
/**
  * ===================================
  * phpfmt
  * ===================================
  */
// "phpfmt.indent_with_space": 2,
/**
  * ===================================
  * PHP Formatter
  * ===================================
  */
// "phpformatter.pharPath": "d:/_Moudle/php-cs-fixer-v2.phar",
// "phpformatter.arguments": [
//   "--rules=psr2"
// ]
/**
  * ===================================
  * Mess
  * The new settings will appear here
  * ===================================
  */
"End Line": "----------------"
```

Last Update on 2017.05.03
