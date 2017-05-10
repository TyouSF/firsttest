---
title: Appium 基础
date: 2017-04-05 10:54:54
categories:
- Appium
tags:
- appium
- 测试
keywords:
---

{% asset_img appium1.png Appium %}

{% cq %}
Appium是一个自动化测试开源工具，支持 iOS 平台和 Android 平台上的原生应用，web 应用和混合应用。

Appium

TyouSF
{% endcq %}

<!-- more -->

----

# Appium 介绍

----

Appium 是一个自动化测试开源工具，支持 iOS 平台和 Android 平台上的原生应用，web 应用和混合应用。

* “移动原生应用”是指那些用iOS或者Android SDK写的原生应用。
* “移动web应用”是指使用移动浏览器访问的应用。
* “混合应用”是指原生代码内嵌H5的形式。比如应用内直接打开网页等。

除此之外，Appium 是一个跨平台的工具：它允许测试人员在不同的平台（iOS，Android）使用同一套API来写自动化测试脚本，这样大大增加了测试套件间代码的复用性。

## Appium理念

为了满足移动自动化需求，Appium 遵循着一种哲学，主要有以下4条：
1. 你无需为了自动化，而重新编译或者修改你的应用。
2. 你不必局限于某种语言或者框架来写和运行测试脚本。
3. 一个移动自动化的框架不应该在接口上重复造轮子。（移动自动化的接口应该统一）
4. 无论是精神上，还是名义上，都必须开源。

## Appium框架

Appium真正的工作引擎其实是苹果和谷歌官方提供的测试框架：

* iOS: 苹果的`UIAutomation`
* Android:  Google的`UiAutomator`

将这些框架封装成一套API--`WebDriver`（也就是 "Selenium WebDriver"） 指定了客户端到服务端的协议。使用这种客户端-服务端的架构，我们可以使用任何语言来编写客户端，向服务端发送恰当的 HTTP 请求。

事实上 WebDriver 已经成为 web 浏览器自动化的标准，也成了 W3C 的标准——[W3C Working Draft](https://dvcs.w3.org/hg/webdriver/raw-file/tip/webdriver-spec.html)

## 概念注解

### C/S 架构

Appium的核心是一个web服务器，它提供了一套接口。它收到客户端的连接，监听到命令，然后在移动设备上按照这些命令执行，然后将执行结果放在HTTP响应中返回给客户端。

### Session

Session我们可以理解为一个上下文链接的对象，我们每次执行测试时，客户端初始化一个seesion（会话）来与服务端交互，之后，我们每一次的运行命令，都将通过这个Session进行后续命令的传达（下发）。

### Desired Capabilities

Desired capabilities是一些键值对的集合（就好比Python中的字典表），客户端将这些键值对发给服务端，告诉服务端我们想要怎么测试。其中所涉及的一些数值，比如：

- `platformName: iOS`：则是告诉Appium服务端，我们测试的应用是ios

等等诸如此类的，可以在后续我们脚本编写中进行更为详细的了解。

### Appium Server

是用Node.js编写的一个服务器。也是我们所编写测试脚本命令所要发送给的对象，经由Appium Server再向测试应用的终端发送执行命令。我们可以用源码编译或者从NPM直接安装。

### Appium Client

Appium Client即我们使用的客户端，也就是我们编写脚本的支持。涉及Java, Ruby, Python, PHP, JavaScript和C#等实现了Appium对WebDriver协议的扩展的语言。我们使用过程中选择一个适合您当前所掌握的语言即可。

----

# Appium 安装

----

以下将介绍Appium如何安装，以及相关环境的配置。如果其中有哪些您已经安装过或者配置过，您可自行忽略。
另：**本文所讲述的安装和配置教程，均是基于Win操作系统，如果您使用的是Mac或其他平台，可查询相关官方文档。**

安装清单：

- JAVA JDK
- Android Studio
- Node.js
- Appium

## JAVA JDK

Android是由Java语言开发的，所以想开发Android应用首先需要Java环境。

JAVA JDK 下载地址：[Java JDK](http://www.oracle.com/technetwork/cn/java/javase/downloads/index-jsp-138363-zhs.html)

{% asset_img JDK1.png %}
{% asset_img JDK2.png %}
{% asset_img JDK3.png %}

### 安装

下载后双击安装文件，进行安装即可，安装时可自行更改安装位置。此处假设您安装时所选路径为：`D:\Java`。

### 配置

接下来，进行环境变量的设置：

1. “我的电脑”右键菜单--->属性--->高级--->环境变量
2. 添加`JAVA_HOME`的变量（变量值根据当前你所安装的JDK目录下的实际版本进行填写）
```
变量名：JAVA_HOME 
变量值：D:\Java\jdk1.8.0_121
```
3. 添加`CLASS_PATH`的变量
```
变量名：CLASS_PATH
变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar; 
```
4. 在Path变量中添加如下两个变量值（非Win10操作系统直接添加：`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`）：
	* `%JAVA_HOME%\bin`
	* `%JAVA_HOME%\jre\bin`

截图参考：↓

{% asset_img JDK4.png %}
{% asset_img JDK5.png %}

### 校验

设置后，在Win下的命令提示符中验证是否配置成功：

1. 打开Win的命令提示符
2. 输入`java -version`
3. 展示如下图所示结果，即证明JAVA JDK配置成功

{% asset_img JDK6.png %}

## Android Studio

有看过其他文章和资料的，相信一定看到过很多需要您安装的，诸如“Android SDK”，“Android ADT”，“Android SDK Platform-Tools”等等很多关于Android环境的安装包。但是其实完全是没有必要的。因为现在最新的Android Studio已经集成上述各种的安装包，无需一一去找和一一安装，我们只需要安装一个最新最全的Android Studio即可。

Android Studio

{% blockquote 维基百科 https://zh.wikipedia.org/wiki/Android_Studio %}
Android Studio是一个为Android平台开发程序的集成开发环境。
{% endblockquote %}

### 安装

访问Android Studio官网进行下载（<https://developer.android.com/studio/index.html?hl=zh-cn>）

{% asset_img androidstudio1.png %}

同样，双击安装包进行安装即可，至于安装路径您可自行更改，这点并不影响。

### 配置Adb

参照下图，添加`ANDROID HOME`的环境变量，以及对应Path下的变量值：

{% asset_img adb1.png %}

### 校验adb

在Win命令提示符下，输入`adb`，如果出现下图所示结果，即证明adb配置成功：

{% asset_img adb2.png %}

## Node.js

### 安装

访问Nodejs官网[nodejs](https://nodejs.org/zh-cn/)，按照下图所示，点击下载即可。
{% asset_img 33114456.png %}
下载完毕后，双击安装包进行安装，安装过程中默认各选项，一直下一步即可。

### 校验

在Win命令提示符下，输入`node -v`，如果出现下图所示结果，即证明node环境OK：

{% asset_img node1.png %}

## Appium

有关Appium的安装，官方首页给出的是使用Node.js进行的安装，但是并不建议使用官方的安装命令，因为在安装过程中，会遇到下载异常问题，而且文件也众多，下载也缓慢。
建议点击主页的下载按钮来直接下载。下载后，是一个zip包，我们解压后，里面会有两个文件：

- appium-installer.exe
- update.bat

### 安装

我们只需要双击`appium-installer.exe`，进行安装即可。
同样的，至于安装在哪里，这完全随您喜欢。

附上安装截图：↓

{% asset_img appium2.png %}
{% asset_img appium3.png %}
{% asset_img appium4.png %}
{% asset_img appium5.png %}
{% asset_img appium6.png %}
{% asset_img appium7.png %}
{% asset_img appium8.png %}

### 校验

#### 通过Appium客户端校验

启动Appium，正常启动后，则展示如下：

{% asset_img appium9.png %}

但是这并不能证明我们的Appium整体环境是否已经搭建成功。接下来，我们在启动Appium后，选择执行Appium按钮之后，如果无异常，应当是如下图所示这样：
{% asset_img appium10.png %}
{% asset_img appium11.png %}

#### 通过`appium-doctor`命令校验

如果您在看本篇教程之前，有看过他人写的一些文章的话，您可能会接触到这样一条校验appium环境是否搭建成功的命令：
```
appium-doctor
```
关于这条命令，并不是所有人都可以直接执行的。首先如果是通过NPM的命令来安装appium的话，笔者并不是很清楚是否可以执行。但是假设您是跟着本教程通过Win下的安装包完成安装的，那么恭喜您：这条命令您并不能直接在Win的命令提示符下执行。执行的时候Win会提示我们这并不是内部或外部命令。
原因：
- 很简单，安装包完成安装后，并没有进行相关环境变量的配置

那么接下来，我们一起看看如何让`appium-doctor`成功运行：

1. **寻找“appium-doctor”**
进入到您安装Appium的目中 --》 会看到有一个文件夹名称为：“node_modules” --》 进入“node_modules”后，会看到有个文件夹名称为：“.bin” --》 进入到“.bin”目录中，您便会发现有一个“appium-doctor.cmd”的文件，恭喜您已经找到了！
2. **配置“appium-doctor”到环境变量”**
将步骤1中“appium-doctor.cmd”的目录进行复制，就像这样一个地址：E:\Appium\node_modules\.bin（具体按照您实际安装的目录进行修改！）。之后进入系统环境变量的Path中进行添加，如图：
{% asset_img appium12.png %}
3. **Win命令提示符下的校验**
配置后，在Win命令提示符中输入`appium-doctor`，如果出现类似下图结果：则证明环境成功搭建完毕。（有任何不成功的，都将会标红并提示出具体还缺少什么环境）
{% asset_img appium13.png %}

----

# 结语

----

相信只要按照本文所述的顺序，进行基本的环境搭建，都应当不会有太大问题。至此，恭喜正在搭建此环境的你，已经成功开启了Appium之旅。接下来，让我们一起看看如何利用‘Python’语言完成我们第一个自动化测试安卓App的Demo脚本吧！

相关学习资料如下（坚持学习，您将能够获得更多的收获）：

> [Python3 中文教程](http://www.runoob.com/python3/python3-tutorial.html)
> [Appium 中文文档](http://appium.io/slate/cn/master/?python#about-appium)
> [Android 调试桥](https://developer.android.com/studio/command-line/adb.html?hl=zh-cn)