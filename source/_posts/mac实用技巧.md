---
title: mac实用技巧
date: 2019-03-18 17:53:04
tags:
 - Mac
---

摘要：
 * 在 Finder 标题栏显示完整路径

<!-- more -->

#### 在 Finder 标题栏显示完整路径
打开终端，输入以下命令并回车：
```
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES
```
然后把 Finder 窗口关了再打开，你会发现有路径栏了。
