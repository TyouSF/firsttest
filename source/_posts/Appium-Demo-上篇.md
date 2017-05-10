---
title: Appium Demo 上篇
date: 2017-04-06 16:28:50
categories:
- Appium
tags:
- appium
- android avd
- 测试
keywords:
---

{% asset_img appium1.png %}

{% cq %}
Pytho + Android AVD + Appium
构建我们的第一个DEMO

TyouSF
{% endcq %}

<!--more-->

本篇内容要旨：

> 主要讲述为了完成我们第一个Demo，所需要完成的基本准备工作。

**声明**：
本Demo主要基于Python语言进行编写，因此，准备工作中的语言库也将围绕Python进行展开。如果您使用的是其他的语言，那么非常抱歉，本文可能并不适合您，建议您通过官网进行相关资料的查询与阅读。

接下来，看看我们都需要哪些吧：

- Python
- Python第三方库--Appium Python Client
- Android AVD（简称安卓模拟器）

----

# Python

----

这是我们基于Python语言编写的基本也是硬性要求了，就不多解释了。
另：
由于本Demo的编写是基于Pyhon3，安装时请务必选择Python3以上的版本。

有关Python的安装，详细可访问[Python 官网](https://www.python.org/)进行下载。
{% asset_img py1.png %}

**友情提示**：
Win操作系统下，为了获得更好的Python支持，在安装Python时，请务必注意一个选项：

- Add python to Path

该选项即是将python添加至系统的环境变量中，这样在安装以后，您便可以在命令提示符中直接使用python相关的命令而无须再进行环境变量的配置。
如果您安装时没在意，没关系，卸载Python后重新安装即可（重新安装时记得选上噢！）。

# Appium Python Client

仅仅是安装Python的语言环境是不够的，我们还要安装Appium的支持库。安装很简单，但是在安装前，不得不提的是：
由于直接安装，可能会导致您当前Python的语言环境不够纯粹。通常情况下，在使用Python的过程中，为了满足不同的项目需求，需要各种第三方库的支持，为了方便管理也为了保持本身Python语言环境的纯粹，会使用沙盒来进行管理和安装。

沙盒：
所谓沙盒环境，是使用Python进行创建的一个基于纯粹Python语言环境下的虚拟环境。在Python中，通常叫做“venv”。安装第三方库便可以在“venv”中进行安装，这样既不会影响我们主题的Python语言环境，也可以为不同的项目创建不同的“venv”环境。

安装Appium Python Client————

1. 在命令提示符下，使用如下命令创建“venv”：
```
python -m venv venv
```
2. 激活虚拟环境
```
venv\Scripts\activate.bat
```
3. 安装Appium Python Client
```
pip install Appium-Python-Client
```

上述总执行过程类似如下图所示：
{% asset_img 461.png %}

# Android AVD（简称安卓模拟器）

由于Demo编写后，需要借助安卓模拟器来展示效果，因此需要安装一下Android AVD。
如果您看过上一篇文章{% post_link "Appium 基础" %}的话，相信基本环境已经搭建完毕了。而我们Android AVD的安装便需要用到Android Studio。

启动Android Studio后，参照下图所示的顺序以及说明进行安装即可。
{% asset_img avd1.png %}
{% asset_img avd2.png %}
{% asset_img avd3.png %}
{% asset_img avd4.png %}
{% asset_img avd5.png %}
{% asset_img avd6.png %}
{% asset_img avd7.png %}

----

# 结语

----

至此，Demo上篇的基本准备工作已经完毕。接下来，让我们一起看看一个Demo是如何编写的吧。
开始前，您可以参照下列资料进行一些自行学习和了解：

> [Appium Python Client](https://github.com/appium/python-client)
> [Python3 教程](http://www.runoob.com/python3/python3-tutorial.html)