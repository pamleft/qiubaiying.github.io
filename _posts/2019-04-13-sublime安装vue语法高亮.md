---
layout:     post
title:      sublime安装vue语法高亮
subtitle:   Vue Syntax Highlight Installed in Sublime
author:     BY
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Blog
---


## 前言

新的一年，好好学习。

## 正文

### 问题来源

最近在看小程序相关的一些内容。

### 问题描述

sublime默认是不支持vue的语法高亮。并且我的sublime不能采用直接install package的方式安装。 

#### 安装内容
首先需要安装[Vue Syntax Highlight](https://github.com/vuejs/vue-syntax-highlight)，这样你的vue文件就能正常显示html，css和js了，另外如果你还在vue文件里写sass，那还得再装个东西，下载[这个](https://codeload.github.com/MarioRicalde/SCSS.tmbundle/legacy.zip/SublimeText2)，解压出来改文件夹名为SCSS，并把这个文件夹放在package目录下，就可以了，记得style标签要加上lang="scss"属性，如果是less，下载[这个](https://codeload.github.com/danro/LESS-sublime/legacy.zip/master)，文件夹名称改为LESS，style标签加上lang="less"

如何找到package目录？  
进入sublime，选择菜单项“Preferences->Browse Packages...”  

如何设置vue语法进行加载？  
按下快捷键“ctrl+shift+p”，在打开的packages输入框中输入vue，选择“Set Syntax:Vue Component”进行加载。  

## 结语
不管怎么样好好加油。
