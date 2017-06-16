---
title: Charles 简明实用教程
date: 2017-05-24 11:02:32
categories:
- 测试工具
tags:
- Charles
- 测试
- 抓包
keywords:
---

{% asset_img charles.png %}

{% cq %}
Charles是一个HTTP代理服务器，HTTP监视器，反转代理服务器。它允许一个开发者查看所有连接互联网的HTTP通信，这些包括request, response和HTTP headers （包含cookies与caching信息）。

百度百科
{% endcq %}

<!-- more -->

# Charles 简述

Charles 是一款非常强大的 HTTP 调试工具，并且兼容几乎所有的平台，可以让开发人员以及测试人员借此来查看到所有设备与服务器之间的 HTTP 以及 SSL/HTTPS 数据交换过程。

然而对于国内的使用者来说，美中不足的是：charles 虽然功能强大，但是却是收费的！

不过这对于我们来说并不是难事，总有办法解决的，你说不是吗？！

Charles 主要的功能包括：

- 截取 Http 和 Https 网络封包。
- 支持重发网络请求，方便后端调试。
- 支持修改网络请求参数。
- 支持网络请求的截获并动态修改。
- 支持模拟慢速网络。

****
# 安装

截至本文发布时，当前 Charles 官网最新版本是4.1.2，相信细心的你在篇头的截图中已经观察到了。

## 下载地址

[Charles 下载](https://www.charlesproxy.com/download/)

在下载页面，可根据自己实际的情况下载对应的版本。本教程将不赘述破解过程，主讲解一些实际使用过程中常用的一些技巧，因此当前即使不破解，使用试用也是可以完成相关的操作的。

## 安装过程

相信你已经是当今冲锋在互联网浪头的老司机了，这样的基础安装相信已经可以不用多说了，根据自己的需要，一路下一步的安装走起吧。

## 界面

charles抓包的显示，支持两种模式，Structure和Sequence。

1. Structure形式如下图 优点：可以很清晰的看到请求的数据结构，而且是以域名划分请求信息的，可以很清晰的去分析和处理数据。
{% asset_img structure.png %}

2. Sequence形式如下图 优点：可以看到全部请求，这里的结果以数据请求的顺序来显示，最新的请求显示在最下面。
{% asset_img sequence.png %}

structure 适合对单一系列的访问请求从宏观上进行把握，可以快速定位。sequence 适合精确定位内容，因为每条sequence 都有size，status等属性信息，方便快速定位这条结果的价值。
笔者在实际使用过程中由于经常要查看相应的数据，并且也知道具体的访问请求，因此常用 structure 结果，大家可以根据实际情况进行具体切换即可。

****
# PC端的使用

**charles会自动配置浏览器和工具的代理设置，所以说打开工具直接就已经是抓包状态了。**

当我们安装完毕启动 charles 时，charles 会进行一些初始化的设定，这个设定我们可以自行在 charles 中根据实际需要来更改，初始的设定下，启动 Charles 后，此时便已经默认监视了 PC 端所有网络数据传输的情况。不信你可以打开 charles 后，使用浏览器访问一些网页，此时这些网页的访问便出现在了 charles 的窗口内。

****
# 移动端使用

想要抓取移动端应用的接口访问情况，使用 Charles 进行一些简单的设定即可。

一下便是设定的步骤：

1. 前提：手机和我们使用 charles 的 PC 应当处于同一个局域网内，这是最基本的要求了。即：手机所连接的热点与电脑所连接的路由是同一个即可；

2. 进入 charles 的代理设定选项中，允许代理，并设定端口号（一般默认8888），如下图：
{% asset_img set01.png %}
{% asset_img set02.png %}

3. 使用 PC 的 cmd 查看本机当前的 ip 地址，然后在手机端的 wifi 代理设置那里去进行相关的配置设置，类似下图：服务器填写 PC 端 ip 地址，端口填写操作2中所设定的代理端口号即可；
{% asset_img set03.png %}

4. 手机设定好，连接成功后，charles 页面便会出现一个是否抓取的相关确认弹窗，我们直接选择允许即可，此时使用手机进行的相关访问数据便可以被监听到了。

**小提示：**
为了更方便的查看手机端的抓包情况，可以关闭掉 PC 上的监听。

****
# 技巧

## 过滤网络请求

通常情况下，我们需要对网络请求进行过滤，只监控向指定目录服务器上发送的请求。

方法——

1. 在主界面的中部的 Filter 栏中填入需要过滤出来的关键字。例如我们的服务器的地址是：http://yourserver.com , 那么只需要在 Filter 栏中填入 yourserver 即可。

2. 在 Charles 的菜单栏选择 “Proxy”->”Recording Settings” 中选择添加一个项目，然后填入需要监控的协议，主机地址，端口号。如下图：
{% asset_img set04.png %}
{% asset_img set05.png %}

3. 在想过滤的网络请求上右击，选择 “Focus”，可以临时性的，快速地过滤出一些没有通过关键字的一类网络请求。

## 截取 Https 通讯信息

通常情况下，如果是测试环境，为了方便测试，多数情况下是没有加密的网络通信，使用 Charles 可以直接抓取到相关的通讯信息，但是正式环境就不行了，没有相关的证书我们也只是能看到访问的地址，而交互的数据等我们是无法查看的。

如果你需要截取分析 Https 协议相关的内容。那么需要安装 Charles 的 CA 证书。具体步骤如下：

1. 点击 Charles 的顶部菜单，选择 “Help” -> “SSL Proxying” -> “Install Charles Root Certificate” 进行证书安装：
{% asset_img set06.png %}

2. Charles 默认也并不截取 Https 网络通讯的信息，如果你想对截取某个网站上的所有 Https 网络请求，可以在该请求上右击，选择 enable SSL proxy，如下图所示：
{% asset_img set07.png %}

## 截取移动设备中的 Https 通讯信息

如果我们需要在 iOS 或 Android 机器上截取 Https 协议的通讯内容，还需要在手机上安装相应的证书。

1. 点击 Charles 的顶部菜单，选择 “Help” -> “SSL Proxying” -> “Install Charles Root Certificate on a Mobile Device or Remote Browser”
{% asset_img set08.png %}

2. 在设备上设置好 Charles 为代理后，在手机浏览器中访问地址：http://charlesproxy.com/getssl ，即可打开证书安装的界面，安装完证书后，就可以截取手机上的 Https 通讯内容了。

**注意：**
默认情况下 Charles 并不做截取，你还需要在要截取的网络请求上右击，选择 SSL proxy 菜单项。

## 模拟慢速网络

在测试过程中，我们也通常会模拟用户真实的 3G， 4G 甚至是 2G 的网络环境下我们应用的真实反馈情况等等，Charles 对此需求提供了很好的支持。

在 Charles 的菜单上，选择 “Proxy”->“Throttle Setting” 项，在之后弹出的对话框中，我们可以勾选上 “Enable Throttling”，并且可以设置 Throttle Preset 的类型。如下图所示：
{% asset_img set09.png %}
{% asset_img set10.png %}

**小提示**：
如果我们只想模拟指定网站的慢速网络，可以再勾选上图中的 “Only for selected hosts” 项，然后在对话框的下半部分设置中增加指定的 hosts 项即可。

## 修改网络请求内容

有些时候为了调试服务器的接口，我们需要反复尝试不同参数的网络请求。Charles 可以方便地提供网络请求的修改和重发功能。

1. 对于以往的网络请求上点击右键，选择 “Compose”，即可创建一个可编辑的网络请求。如下所示：
{% asset_img set11.png %}

2. 新建一个自定义的请求，可以在 “Tools”->“Compose a new request” 或中进行设置：
{% asset_img set12.png %}

有了请求后，们可以修改该请求的任何信息，包括 URL 地址、端口、参数等，之后点击 “Execute” 即可发送该修改后的网络请求。 Charles 支持我们多次修改和发送该请求，这对于我们和服务器端调试接口非常方便。

## 给服务器做压力测试

我们可以使用 Charles 的 Repeat 功能来简单地测试服务器的并发处理能力，方法如下。
我们在想打压的网络请求上（POST 或 GET 请求均可）右击，然后选择 「Repeat Advanced」菜单项，如下所示：
{% asset_img set13.png %}

接着我们就可以在弹出的对话框中，选择打压的并发线程数以及打压次数，确定之后，即可开始打压。

{% asset_img set14.png %}

## 修改服务器返回内容

有些时候我们想让服务器返回一些指定的内容，方便我们调试一些特殊情况。例如列表页面为空的情况，数据异常的情况，部分耗时的网络请求超时的情况等。如果没有 Charles，要服务器配合构造相应的数据显得会比较麻烦。这个时候，使用 Charles 相关的功能就可以满足我们的需求。

根据具体的需求，Charles 提供了 Map 功能、 Rewrite 功能以及 Breakpoints 功能，都可以达到修改服务器返回内容的目的。这三者在功能上的差异是：

- Map 功能适合长期地将某一些请求重定向到另一个网络地址或本地文件。
- Rewrite 功能适合对网络请求进行一些正则替换。
- Breakpoints 功能适合做一些临时性的修改。

### Map 功能

Charles 的 Map 功能分 Map Remote 和 Map Local 两种，顾名思义，Map Remote 是将指定的网络请求重定向到另一个网址请求地址，Map Local 是将指定的网络请求重定向到本地文件。

在 Charles 的菜单中，选择 “Tools”->”Map Remote” 或 “Map Local” 即可进入到相应功能的设置页面。
{% asset_img set15.png %}

对于 Map Remote 功能，我们需要分别填写网络重定向的源地址和目的地址，对于不需要限制的条件，可以留空。下图是一个示例，我将所有 testserver.com（测试服务器）的请求重定向到了 www.releaseserver.com（线上服务器）。
{% asset_img set16.png %}

对于 Map Local 功能，我们需要填写的重定向的源地址和本地的目标文件。对于有一些复杂的网络请求结果，我们可以先使用 Charles 提供的 “Save Response…” 功能，将请求结果保存到本地（如下图所示），然后稍加修改，成为我们的目标映射文件。
{% asset_img set17.png %}

下图是一个示例，我将一个指定的网络请求通过 Map Local 功能映射到了本地的一个经过修改的文件中。
{% asset_img set18.png %}

Map Local 在使用的时候，有一个潜在的问题，就是其返回的 Http Response Header 与正常的请求并不一样。这个时候如果客户端校验了 Http Response Header 中的部分内容，就会使得该功能失效。解决办法是同时使用 Map Local 以下面提到的 Rewrite 功能，将相关的 Http 头 Rewrite 成我们希望的内容。

### Rewrite 功能

Rewrite 功能功能适合对某一类网络请求进行一些正则替换，以达到修改结果的目的。
例如，我们的客户端有一个 API 请求是获得用户昵称，而我当前的昵称是 “tangqiaoboy”，如下所示：
{% asset_img set19.png %}

我们想试着直接修改网络返回值，将 tangqiaoboy 换成成 iosboy。于是我们启用 Rewrite 功能，然后设置如下的规则：
{% asset_img set20.png %}

完成设置之后，我们就可以从 Charles 中看到，之后的 API 获得的昵称被自动 Rewrite 成了 iosboy，如下图所示：
{% asset_img set21.png %}

### Breakpoints 功能

上面提供的 Rewrite 功能最适合做批量和长期的替换，但是很多时候，我们只是想临时修改一次网络请求结果，这个时候，使用 Rewrite 功能虽然也可以达到目的，但是过于麻烦，对于临时性的修改，我们最好使用 Breakpoints 功能。
Breakpoints 功能类似代码调试时的断点一样，当指定的网络请求发生时，Charles 会截获该请求，这个时候，我们可以在 Charles 中临时修改网络请求的返回内容。
下图是我们临时修改获取用户信息的 API，将用户的昵称进行了更改，修改完成后点击 “Execute” 则可以让网络请求继续进行。
{% asset_img set22.png %}

{% note danger %}**注意点**：{% endnote %}
使用 Breakpoints 功能将网络请求截获并修改过程中，整个网络请求的计时并不会暂停，所以长时间的暂停可能导致客户端的请求超时。

****
# 结语

关于 Charles 的简明实用教程，目前就先写这么多吧，希望在以后的实际使用过程中，大家通过不断的练习和使用，早日成为老司机。


让我们一起共勉：
> 持续不断地学习，是更好的成长 ---TyouSF

****
# 参考资料

----

> [Charles 官网](https://www.charlesproxy.com/)
> [Charles 官网文档](https://www.charlesproxy.com/documentation/)