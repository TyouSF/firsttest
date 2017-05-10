---
title: GitHub Pages + Hexo & NexT 快速构建静态Blog
categories:
- Hexo
tags:
- github pages
- hexo
- next
date: 2017-03-30 16:46:19
keywords:
---


写在本博客搭建完毕之初

---

本文旨在快速让各位读者拥有属于自己的静态博客，相信纯属小白不懂代码的读者，只要按照如下所述的步骤进行操作，瞬间即可拥有自己的个人免费静态博客。

所涉及到的工具有：

- Git
- Node.js
- Hexo
- NexT

<!--more-->

# 从GitHub开始，拥有一个不完美的站点

有关GitHub尚不清楚的小伙伴，可自行百度，进行更详细的了解。  
这里只进行简单的介绍和说明：

{% blockquote 维基百科 https://zh.wikipedia.org/wiki/GitHub %}
GitHub是一个通过Git进行版本控制的软件源代码托管服务，由GitHub公司（曾称Logical Awesome）的开发者Chris Wanstrath、PJ Hyett和Tom Preston-Werner使用Ruby on Rails编写而成。
{% endblockquote %}

## 注册GitHub

访问[GitHub](https://github.com/)主页，进行基本的GitHub账户注册，此时，面前的你可能会面临一个问题————  
由于国内的“**防火长城**”，GitHub网站有可能无法访问。有过科学上网经验的小伙伴一定不陌生，使用我们的科学上网姿势，即可访问。如果面前的你对科学上网尚且一无所知，那也没有关系，自行百度“科学上网”，总能找到一款适合您的解决方案。如果你没有更好的选择，那么我个人推荐使用[Shadowsocks](http://abc.ishadow.online/)，打开网站后，切换为中文，按照官网的教程，相信您马上就可以get到科学上网的姿势。

解决墙的问题后，访问GitHub，并完成注册即可。

注册页面见：↓
{% asset_img github-signup.png signup for git %}

## 快速拥有一个不完美的站点

完成注册后，按照下图的顺序，完成各个步骤的操作：

1. 进入到我们的个人资料
{% asset_img 33114451.png your profile %}

2. 进入我们的git仓库
{% asset_img 33114452.png your repositories %}

3. 新建一个远程Git代码仓库
{% asset_img 33114453.png new repositories %}

4. 新建我们的博客托管仓库
此处，我们假设你注册时的github的用户名为：yourname，创建一个`yourname.github.io`的仓库，具体可参照下图。
{% asset_img 33114454.png create repositories %}

5. 创建完毕后，恭喜您，您已经拥有了个人站点，虽然还不完美。

通过在浏览器中输入我们操作4中创建的仓库名，即可访问到。  
举个例子——
我们按照操作4中假设的名称创建的话，那么您访问的地址应当是：<https://yourname.github.io/>。各位读者只需要把`yourname.github.io`换成您创建仓库时所填写的对应名称即可。

----

# 搭建Hexo，让我们的站点更为完美

关于Hexo的搭建，您可以参考Hexo官网，点此→[Hexo](https://hexo.io/zh-cn/)，阅读更为详细的文档说明。如果您使用的是mac，那么请对照Hexo的官方文档进行搭建，本文主要介绍Windows操作系统上的搭建和使用（请各位读者谅解）。

## 认识Hexo
{% blockquote Hexo https://hexo.io/zh-cn/docs/ 什么是Hexo %}
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
{% endblockquote %}

## 环境搭建

### 安装Git

看过前面的教程后，大家已经使用过Git，等等，那不是一个网页吗，怎么还需要安装Git了？没错，我们是要安装，原因是，您所访问的是Git的远程仓库托管，但是本地化的Git才是用于我们代码管理的本质，因此我们需要安装一个本地的Git管理工具。

可以访问Git工具的官网[Git](https://git-scm.com/)，和前面所介绍的一样，可能会遇到墙的问题，此处不再细说，可参照前文所写。

登录后，官网点击下载即可，详细如下图：
{% asset_img 33114455.png git download %}
下载完毕后，双击安装包进行安装，安装过程中默认各选项，一直下一步即可。

### 安装Node.js

访问Nodejs官网[nodejs](https://nodejs.org/zh-cn/)，按照下图所示，点击下载即可。
{% asset_img 33114456.png nodejs download %}
下载完毕后，双击安装包进行安装，安装过程中默认各选项，一直下一步即可。

### 安装Hexo

安装完Git后，在桌面空白地方，点击鼠标右键，可发现菜单栏中存在名为`Git Bash Here`的可选项，我们选择它即可开启我们的git命令行操作界面

> 选择`Git Bash Here`
{% asset_img 33114457.png click Git Bash Here %}

> 启动`Git Bash Here`后的界面
{% asset_img 33114458.png Git Bash UI %}

> 安装Hexo  
在打开的Git Bash界面内，我们输入如下的命令即可完成Hexo的安装
* `npm install -g hexo-cli`

## Hexo & NexT 让我们的博客更完美

### 使用Hexo与NexT

通常我们会有如下的操作来初始化我们的hexo博客，请打开我们的GitBash，在命令行中输入下列的命令：

1. `cd d:`  
用于切换到指定盘符下，随您喜欢（建议找一个您方便查看的盘符下）
2. `hexo init yourfilename`
yourfilename是您指定的文件夹名称（建议英文名，如果您没有好的名字，可以试试“myblog”）
3. `cd yourfilename`  
进入到我们hexo初始化的文件夹目录下
4. `npm install`  
完成安装
5. `git clone https://github.com/iissnan/hexo-theme-next themes/next`  
下载NexT主题
6. 打开位于站点(yourfilename)根目录下`_config.yml`文件，找到 theme 字段，并将其值更改为 next
7. 回到GitBash界面，使用`hexo server`启动我们的站点
8. 启动后，打开浏览器，输入：`localhost:4000`即可看到我们本地启动的博客

到此为止，恭喜您，已经成功的让自己的博客运行起来了。

## 部署本地的博客站点到GitHub上

### 配置Git

1. 安装`hexo-deployer-git`,在GitBash中使用如下命令  
`npm install hexo-deployer-git --save`
2. 在站点根目录下的`_config.yml`中修改配置
```
deploy:
  type: git
  repo: <repository url>
  branch: master
  message: 
```  
获取`repository url`,可参照下图：{% asset_img 33114459.png get repository url %}
3. `hexo deploy`  
执行后，按照提示输入git账户与密码后，即可完成部署

此时访问您的站点：<https://yourname.github.io/>即可看您搭建好的博客

**感谢您的坚持，同时恭喜您，您的博客已经搭建好了**

# 后续

本博客搭建也好，还是后续的文章编写等，都涉及到命令行，因此需要各位读者在后续的时间里，对Hexo的命令，以及Git的命令都要有所了解，同时还要对Markdown的语法有一定的了解，能够编写最基本的Markdown语法的文章。相关学习资料如下（坚持学习，您将能够获得更多的收获）：

> [Git 简体中文版](http://iissnan.com/progit/)
> [Hexo 文档](https://hexo.io/zh-cn/docs/)
> [Markdown 入门参考](http://xianbai.me/learn-md/index.html)
> [NexT 使用指南](http://theme-next.iissnan.com/getting-started.html)