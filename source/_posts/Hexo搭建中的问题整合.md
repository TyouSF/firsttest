---
title: Hexo搭建中的问题整合
date: 2017-03-31 16:01:21
categories:
- Hexo
tags:
keywords:
---

前序

> 本文旨在对于Hexo搭建过程中，遇到的一些问题的整理，希望也能帮助正在阅读的你，解决一些疑惑

# 关于npm命令

## npm命令安装第三方插件时的执行路径

使用过Hexo后，我们会发现，前端页面显示通常仅仅支持了简易的markdown语法，如果要扩展在网页中呈现更高级的markdown语法特性，我们便要去寻找扩展的插件。

<!--more-->

幸运的是，Hexo官网已经为我们提供了官网的一些可能会用到的插件，我们需要按照官网的链接去寻找，并按照对应的安装方式进行安装即可，这里附上Hexo官方插件查询地址：[Hexo 插件](https://hexo.io/plugins/)

**注意**:
我们在安装任何第三方的插件库来扩展我们的站点时，请务必在我们的站点根目录下执行相应的安装命令。
假设——
我们的站点，安装在`D`盘，名为`myblog`的文件夹下，我们想要让我们的站点支持页面的脚注功能，对应的插件名为`hexo-footnotes`,首先启动GitBash，然后我们应当这么执行：
```
yourpcname@DESKTOP-OLULDAI MINGW64 ~
$ cd d:
yourpcname@DESKTOP-OLULDAI MINGW64 /d
$ cd myblog
yourpcname@DESKTOP-OLULDAI MINGW64 /d/myblog
$ npm install hexo-footnotes --save
```
如果你发现安装的插件不起作用，一定要确认是否是在站点目录下执行的安装命令。

## 学会利用`hexo clean`的命令

如果你发现，你新修改的主题以及样式，没有展示为最新的，可以使用该命令清除数据之后，再次启动或者重新生成站点后再提交至Git。

## 使用`hexo deploy`自动部署遇到问题

通常使用自带的部署命令可能会存在一些问题，官方也有提及。所以遇到问题之后，建议回归到Git的本质，来使用原生的Git命令来提交。那么问题来了：

1. 我们该把什么作为我们的博客文件提交至Git呢？
2. 我们该怎么管理我们本地仓库与远程Git仓库呢？

第一个问题：
其实真正需要我们提交至Git，作为我们博客的文件，是我们hexo搭建的站点跟目录下的`public`文件夹内的所有文件。每当我们要发布最新的博文时，我们就先使用`hexo generate`来生成`public`文件夹。
第二个问题：
建议通过克隆我们远程的站点仓库，来创建我们的本地站点仓库。假设我们在d盘下执行：
```
yourpcname@DESKTOP-OLULDAI MINGW64 ~
$ cd d:
yourpcname@DESKTOP-OLULDAI MINGW64 /d
$ git clone git@github.**....
```
执行后，我们本地D盘就会有一个Git仓库，里面存放着我们的远程站点内容。此时我们可以将最新的`public`文件夹内的所有文件拷贝到这里之后，使用如下命令来完成部署：
```
yourpcname@DESKTOP-OLULDAI MINGW64 /d
$ cd yourname.github.io
yourpcname@DESKTOP-OLULDAI MINGW64 /d/yourename.github.io
$ git add .
yourpcname@DESKTOP-OLULDAI MINGW64 /d/yourename.github.io
$ git commit -m '***'
yourpcname@DESKTOP-OLULDAI MINGW64 /d/yourename.github.io
$ git push
```

# 关于Hexo的一些提醒事项：

Hexo所搭建的博客是静态的，同时GitHubPages虽然是我们的站点博客，但同时也是公开的，因此：

* 任何人都可以看到我们博客的仓库原文件，因此，**切勿存放以及暴露个人隐私数据**；
* 任何人都可以看到我们博客的仓库原文件，因此，**切勿存放以及暴露个人隐私数据**；
* 任何人都可以看到我们博客的仓库原文件，因此，**切勿存放以及暴露个人隐私数据**；