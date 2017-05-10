---
title: Python3 环境
date: 2017-04-24 14:51:24
categories:
- Python
tags:
- python
keywords:
---

{% asset_img python.png %}

{% cq %}
--本篇主要讲述 Python的环境--

“优雅”    “明确”    “简单”
Python
{% endcq %}

<!--more-->

简要：

以介绍Python的基本安装，和编写Python的一些基本工具的使用和介绍。

----

# Python3 环境搭建

----

## 安装

请访问官网自行下载Python3的安装包：[Python 官网](https://www.python.org/)。

注意：
请下载Python3.0以上版本，因为我们讲述的是基于Python3的内容!
请下载Python3.0以上版本，因为我们讲述的是基于Python3的内容!
请下载Python3.0以上版本，因为我们讲述的是基于Python3的内容!

截至本文编写完毕时，当前Python3的最新版本为：3.6.1

安装过程中，可根据需要，自行更改安装位置，但是有一点，请务必勾选一个选项：

* "Add Python3.6 to PATH"

这个选项是将Python添加至环境变量，便于在命令行中启用Python命令提示符。

附简略安装截图：

{% asset_img python1.png %}
{% asset_img python2.png %}
{% asset_img python3.png %}

## 校验

启用Win操作系统的命令提示符，输入python可校验，安装成功如下图：

{% asset_img python4.png %}

----

# Python3 IDE工具

----

基本的Python环境搭建完毕后，接下来便是编写Python的程序。

大多数的编程语言都有着各式各样的编程工具，大多也都是以IDE著称。

那么什么是IDE呢：

> IDE 集成开发环境（Integrated Development Environment，简称IDE，也称为Integration Design Environment、Integration Debugging Environment）

简言之即为：辅助程序开发人员开发软件的应用软件，在开发工具内部就可以辅助编写源代码文本、并编译打包成为可用的程序，有些甚至可以设计图形接口。

然而由于Python的语言较为简单易学易用，对于大牛来说，可能一个简单的记事本便可搞定基本的Python开发。
但是毕竟还是有局限的，所以这里推荐几款在日后我们编写Python的过程中常用或者说比较好用的几款工具，供大家参考和学习。

- [Sublime Text](https://www.sublimetext.com/)
- [PyCharm](https://www.jetbrains.com/pycharm/)

## Sublime Text

Sublime Text是一个插件丰富支持多种语言的编辑器。当前版本最新的叫：Sulime Text3

而且我个人也推荐使用 Sublime Text3 版本，至于 Sublime Text2还是不建议使用的，因为 Sublime Text2 中集成的是 Python 2.7的版本，并不适用我们使用的 Python3。

上面已经给出了官网地址，可自行前往下载并安装使用。

安装完毕后，为了更好的使用 Sublime Text3 编写 Python 程序，有一些插件还是要推荐给大家安装的：

* Package Control 【Sublime中插件管理工具】
* SideBarEnhancements 【Sublime侧边栏扩展工具】
* AutoPEP8 【Python编码pep8规范】
* SublimeREPL 【可在Sublime中直接运行Python环境】
* Anaconda 【自动匹配关键字等实用功能】

更多可用插件可自行查阅相关资料，这里就不一一赘述了。

----

# 结语

----

有关基本Python的环境以及IDE工具介绍就到此为止了，其实工具有很多，重要是的Python代码使用的熟练度和实际项目经验。最后记录相关更多的资料和工具推荐，可详见参考部分。

----

# 参考

----

> [Python 官网](https://www.python.org/)
> [Sublime Text 官网](https://www.sublimetext.com/)
> [PyCharm 官网](https://www.jetbrains.com/pycharm/)
> [ATOM 官网](https://atom.io/)
> [Notepad++ 官网](https://notepad-plus-plus.org/)
> [Package Control 官网](https://packagecontrol.io/) Sublime Text的插件管理工具