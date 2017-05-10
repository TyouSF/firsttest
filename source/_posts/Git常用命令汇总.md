---
title: Git常用命令汇总
date: 2017-04-14 14:59:45
categories:
- Git
tags:
- git
keywords:
---

{% asset_img git1.png %}

{% cq %}
自诞生于 2005 年以来，Git 日臻成熟完善，在高度易用的同时，仍然保留着初期设定的目标。 它的速度飞快，极其适合管理大项目，有着令人难以置信的非线性分支管理系统
Git 简史
{% endcq %}

<!--more-->

Git是什么，就不多介绍了，相关的资料和度娘的解答相信已经多的数不胜数了。本文主要来讲述我们实际工作中常用的一些基本命令以及使用的汇总。具体和详细的教程以及原理的东西可以参考本文最后给出的资料，个人认为这些资料已经足以阐释很多东西了。废话不多说，进入正文：Git常用命令一览！

在介绍前，先明确两个基本概念（大牛请直接忽略此处）：

1. 本地仓库  
在你所使用的电脑上进行创建和管理的仓库，我们称之为本地仓库

2. 远程仓库  
在GitHub网站上托管的仓库，我们称之为远程仓库

3. 代码内须填参数“< >”  
在代码中凡是用尖括号“< >”括起来的则是需要我们填写的具体参数，实际使用中，尖括号不用书写

4. origin 代指远程仓库在本地显示的名称  
如果没有特殊情况，origin代之远程仓库的名称，这是git默认的名称。

----

# Git 基本配置

----

* 配置全局git用户名
```
git config --global user.name "yourname"
```

* 配置全局git用户邮箱地址
```
git config --global user.email yourmail@example.com
```

* 查看配置信息
```
git config --list
```

----

# Git 本地仓库的初始化

----

* 将当前所在的根目录文件夹直接变为git仓库
```
git init
```

* 在当前的路径下，新建一个我们命名的文件夹，并将其初始化为git仓库
```
git init foldername
```

----

# Git 提交管理

----

* 提交前，查看当前文件状态
```
git status
```

* 将某一具体的新增或有修改的代码文件添加至暂存区等待提交
```
git add filename
```

* 将某一具体的已添加至暂存区的文件从暂存区移除
```
git reset HEAD filename
```

* 批量添加所有新增或有变更的文件至暂存区等待提交
```
git add .
```

* 将暂存区的文件提交至当前分支，并添加本次提交的注释
```
git commit -m "comments for your commit"
```

* 撤销刚才的提交并重新编辑注释后再次提交
```
git commit --amend
```

* 跳过添加暂存区直接进行提交
```
git commit -a -m "comments for your commit"
```

* 查看提交历史
```
git log
```

----

# Git 文件管理

----

* 从工作目录中手工删除文件
```
rm filename # 移除文件
git rm filename # 在暂存区记录此次的移除操作
```

* 移动并重命名文件
```
git mv file_from file_to
```

----

# Git 本地分支管理

----

注意事项：

在使用本地分支管理之前，请确保你所创建的本地仓库并不是空的，且有过提交历史，否则可能无法顺利创建分支。

* 创建新的分支
```
git branch <new_branch>
```

* 切换到某个分支
```
git checkout <branch>
```

* 创建新的分支并切换到新建的分支
```
git checkout -b <new_branch>
```

* 基于现有分支创建新分支并切换过去
```
git checkout -b <new_branch> <branch>
```

* 查看当前所有分支
```
git branch
```

* 将某一分支合并到当前分支
```
git merge <branch>
```

* 查看各个分支最后提交信息
```
git branch -v
```

* 查看已经被合并到当前分支的分支
```
git branch --merged
```

* 查看尚未被合并到当前分支的分支
```
git branch --no-merged
```

* 安全删除分支（如果该分支并未被合并，删除该分支会提示错误，因为那样做会丢失数据）
```
git branch -d <branch>
```

* 强制删除某个分支（未被合并的分支被删除的时候需要强制）
```
git branch -D <branch>
```

----

# 远程仓库管理

----

* 给本地仓库添加一个远程仓库
```
git remote add <shortname> <url>
```

* 修改远程仓库地址
```
git remote set-url <shortname> <new_url>
```

* 克隆远程仓库到本地新仓库
```
git clone <repository_url>
```

* 查看当前的远程仓库
```
git remote
```

* 查看远程仓库状态
```
git remote show origin
```

* 删除本地添加的远程仓库
```
git remote rm <shortname>
```

* 重命名本地的远程仓库名
```
git remote rename <shortname> <new_shortname>
```

----

# 远程分支管理

----

* 首次提交本地分支至远程分支（如无远程主分支则创建，用于初始化远程仓库）
```
git push -u origin <branch>
```

* 非首次提交至远程分支（默认自动提交至当前本地分支所对应的远程分支）
```
git push
```

* 抓取远程仓库所有分支更新并合并到本地
```
git pull
```

* 抓取远程仓库所有分支更新并合并到本地，不要快进合并
```
git pull --no-ff
```

* 抓取远程仓库更新
```
git fetch origin
```

* 将远程分支合并到本地当前分支
```
git merge (远程仓库名)/(远程分支名)
```

* 跟踪某个远程分支创建相应的本地分支
```
git checkout --track <origin>/<branch>
```

* 删除远程分支，origin是远程仓库名
```
git push origin :<branch>
```

----

# 本地分支与远程分支关联

----

* 绑定远程和本地分支
```
git branch --set-upstream <local_branch> <origin>/<origin_branch>
```

----

# SSH公钥

----

* 生成 SSH 公钥
```
ssh-keygen
```

----

# 结语

----

通过上述的一些命令，我们日常git的使用基本没有什么问题了。但是实际使用过程中可能会遇到诸多的问题，顿时很是疑惑，也不知该如何解决。相信在您使用上一段时间后，肯定会遇到的。这个时候我们要多查找一些官方文档或者资料，多学习多看多实践，相信一定可以得到解决。如果有时间，建议了解一下Git的一些底层和原理性的东西，更能加深我们对Git的理解。

----

# 参考资料

----

> [Pro Git 简体中文版](http://iissnan.com/progit/)
> [Git 简易指南](http://www.bootcss.com/p/git-guide/)
> [Git 实操学习站点](http://learngitbranching.js.org/)