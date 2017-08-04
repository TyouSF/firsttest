---
title: Git中多个sshKey的管理
date: 2017-06-01 09:53:10
categories:
- Git
tags:
- git
keywords:
---


# 在使用Git时，我们很多时候会遇到这样的问题

- 公司有一个 Git 仓库，我们需要持续的完成工作中所需要完成的任务并提交代码
- 个人自己平时做的一些小项目，写的小工具，在 Git 上托管，我们需要提交
- ...或者我们自己接了一些外包的项目，需要提交至外包项目的 Git 中

这个时候，如果邮箱都一样，那么自然不需要去管理多个 sshkey 。但是大多数的情况下，
我们更期望或者实际工作中更为现实的是，每一个不同的项目，我们都会有不同的邮箱来管理
和提交。

**问题**
如何去管理多个 sshkey 呢？
这也就是我们本文要解决的问题。
<!--more-->

# 具体实操

废话不多说，直接上操作：

根据官文，通常生成一个 sshkey 只需要 gitbash 中输入如下命令：
```
ssh-keygen
```

上述生成的是默认的 key 文件，在没有其他配置的情况下，通常所有的 git 仓库提交内容都会优先
使用该命令生成的公钥，对应的文件名称是：“id_rsa” 与 “id_rsa.pub”。

因为我们需要为不同的 git 仓库来配置不同的 sshkey，因此我们在生成 sshkey 的时候，就不能够再
使用上述的简化命令了。

> 第一步

为了简化我们的操作，我们可以使用更为完善的命令，如下↓：
```
ssh-keygen -t rsa -C "yourmail@gmail.com" -f ~/.ssh/sshname
```
例如，我们在公司使用的邮箱是 mycompany@mail.com ，我们期望公司使用的 sshkey 名为“mycompany”，那么
我们的命令便是(其中，“mycompany” 文件名前的 `~/.ssh/` 是我们存放 sshkey 的路径也是默认 git 存放的路径)：
```
ssh-keygen -t rsa -C "mycompany@mail.com" -f ~/.ssh/mycompany
```

> 第二步

用同样的方法，我们可以继续为其他项目生成相应的 key，
此处假设我们生成的第二个 key 的名称为：“mygit”

> 第三步

配置 config 文件--
进入到 git 中存放 sshkey 的目录下，即 `~/.ssh/` 目录下，创建一个 config 文件。

创建 tips：
1. 在windows下新建一个txt文本，然后将名字后缀一起改成config即可
2. 在bash下的话直接touch config 即可

假设公司的 git 地址是：`code.company.io`
自己在 github 的项目地址是：`github.com`
并且假设我们公司的用户名叫：`companynick`
自己在 github 的用户名是：`mynick`

那么添加的内容如下↓：
```
# gitcompany // 新 host 的称呼
	Host code.company.io // 主机名字，不能重名
    	HostName code.company.io  // 主机所在域名或IP
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/mycompany // 私钥路径
        User companynick // 用户名称

# github
    Host github.com
        HostName github.com
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/mygit
        User mynick
```

> 第四步

在公司的 git 以及自己的 github 中添加各自对应的公钥。

> 第五步

测试连接是否成功，成功则证明我们的配置已经完成了，就可以在以后提交的时候使用不同的配置。
测试连接命令：
```
ssh -T git@github.com
```

**测试连接地址 tips**
可以在仓库克隆的地址中得到。

最后，有关全局配置的说明：

取消全局配置信息--
```
git config --global --unset user.name
git config --global --unset user.email
```

单个 git 仓库下配置特定的 username 与 email--
```
git config user.name "yourname"
git config user.email "youremail"
```

----


让我们一起共勉：
> 持续不断地学习，是更好的成长 ---TyouSF

****

# 参考资料

----

> [Pro Git 简体中文版](http://iissnan.com/progit/)
> [Git 简易指南](http://www.bootcss.com/p/git-guide/)
> [Git 实操学习站点](http://learngitbranching.js.org/)