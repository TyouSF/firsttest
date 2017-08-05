---
title: Locust性能测试初探
date: 2017-08-04 16:57:00
categories:
- Locust
tags:
- python
- locust
- 性能测试
keywords:
---

{% asset_img locust.png %}

{% cq %}
An open source load testing tool.

Define user behaviour with Python code, and swarm your system with millions of simultaneous users.

--Locust
{% endcq %}

<!--more-->

# 前述

----

到目前为止，对于性能测试的实践其实也并不是很多。为了弥补这片空白，也是各种找资料学习。
网上关于性能测试资料最多的，其实大家一搜索便知道一二，其中：

1. loadrunner
2. Jmeter

这两款工具也是目前能够检索到相关资料较多的测试工具，这两者的区别也很明显：

1. loadrunner 是一款商用软件，需要收费，相比之下，Jmeter 则是开源免费的
2. 二者的并发机制有所不同，想更深入的同学可自行了解，此处不多述

## 性能测试

引用百度的介绍————

> 性能测试是通过自动化的测试工具模拟多种正常、峰值以及异常负载条件来对系统的各项性能指标进行测试。负载测试和压力测试都属于性能测试，两者可以结合进行。通过负载测试，确定在各种工作负载下系统的性能，目标是测试当负载逐渐增加时，系统各项性能指标的变化情况。压力测试是通过确定一个系统的瓶颈或者不能接受的性能点，来获得系统能提供的最大服务级别的测试。

## Locust的发现

由于自己也想更多的弥补这方面的空白，因为在调查性能测试工具的过程中，无意间发现了 Locust 这样一个开源的框架，
进一步仔细看后，发现 Locust 使用的是 python 语言编程实现的，恰巧本小白现在也刚好正在主要使用 python，因此
二话不说，就学起来，重点是：Locust 也是免费开源的啊，而且目前国内对其的了解和使用也相对较少，说不定以后小白
就走在了国内的前沿了呢，有木有很厉害，那就赶紧跟我一起学起来吧！！！

----

# Locust 初探

----

以下内容其实也纯属搬砖，为什么这么说呢，因为这些都源自官方文档，没有耐心看英文，想要快速一睹 Locust 真面目的
不妨就来看看，让我们快速窥探 Locust 吧。

## Locust 安装

整个安装和检测等，都是在 python shell 下完成的：

- 在 python shell 命令下，使用 pip 完成快速安装：
```
pip install locustio
```

- 安装完成后，检测是否安装成功：
```
locust --help
```

- 如果你想使用 locust 更为强大的分布式性能测试，那么还需要安装 `pyzmq`
```
pip install pyzmq
```

### 注意事项

操作系统不同，安装的方式有所不同，并且安装后可能都会遇到一些问题，请详细查看下方内容，减少走弯路。

#### 当前版本的问题

* `ModuleNotFoundError: No module named 'core'` 的错误

当前情况下，无论是在 windows，还是 linux/macos，在当前的 locust 版本下，安装后，可能存在无法使用的问题，
这个问题是在使用 `locust --help` 会提示 `ModuleNotFoundError: No module named 'core'` 的错误，这种
问题是当前 locust 的一个 bug， 在 locust git项目中，可以查到相应的解决方案，遇到此问题，解决方式是：

1. `pip uninstall locustio` 先卸载安装的 locust
2. `pip install locustio==0.8a2` 使用新的安装命令安装
3. `locust -f locustfile.py` 再次检测，会发现，已经解决了问题 ✌

* Windows 平台下安装的问题

从官方文档中，很清楚的提及操作系统的问题，官方推荐是建议在 Linux/Mac OS 上使用，其中原因是对于操作系统内核  
的使用兼容上。
因此，在 Win 平台下安装，会遇到安装失败的问题，通常是需要安装 `Visual C++` 的。因此安装前请确认 Visual C++  
各系列是或否都已经安装。

如果不确定，那么久按照失败的提示，访问 Visual C++ 官网 [Visual C++](http://landinghub.visualstudio.com/visual-cpp-build-tools) 下载安装

安装后再使用上述安装命令就可以发现，安装OK ✌ 了

## Locust 快速示例

根据官方文档，快速示例有两种写法，区别是在于对于用户行为定义的两种不同形式，一种是采用 tasks 参数，指定用户行为；一种是采用 @task 装饰器，在用户行为类内部定义。

1. 第一种，单独定义行为函数，采用 tasks
```
from locust import HttpLocust, TaskSet

def login(l):
    l.client.post("/login", {"username":"ellen_key", "password":"education"})

def index(l):
    l.client.get("/")

def profile(l):
    l.client.get("/profile")

class UserBehavior(TaskSet):
    tasks = {index: 2, profile: 1}

    def on_start(self):
        login(self)

class WebsiteUser(HttpLocust):
    task_set = UserBehavior
    min_wait = 5000
    max_wait = 9000
```

2. 行为类内部，采用 @task 装饰器定义
```
from locust import HttpLocust, TaskSet, task

class UserBehavior(TaskSet):
    def on_start(self):
        """ on_start is called when a Locust start before any task is scheduled """
        self.login()

    def login(self):
        self.client.post("/login", {"username":"ellen_key", "password":"education"})

    @task(2)
    def index(self):
        self.client.get("/")

    @task(1)
    def profile(self):
        self.client.get("/profile")

class WebsiteUser(HttpLocust):
    task_set = UserBehavior
    min_wait = 5000
    max_wait = 9000
```

二者无论采用哪种，都是一样的，但是官方推荐使用的是 @task 装饰器的形式。

## 启动运行

如果上述脚本的名称为 “locustfile.py” 那么我们便可以直接运行如下命令，启动脚本：
```
locust --host=http://example.com
```

如果脚本名称不是 locust 默认支持的，那么运行的时候也需要指定脚本文件：
```
locust -f locust_files/my_locust_file.py --host=http://example.com
```

## 访问 locust 网页

成功启动可以到如下的命令提示：
```
Starting web monitor at *:8089
Starting Locust 0.8a2
```

通过如下地址即可访问：
```
http://localhost:8089/
```

打开 locust 实时监控的页面后，我们首先需要操作的便是配置：
- 并发用户数
- 产生模拟用户的速度

配置后，即可进入实时监控页面，看到各个响应的性能指标等

----

# 结语

----

相信通过上述的内容，小伙伴们都已经掌握了基本的 locust 的使用，接下来的内容中我们将逐一介绍 locust 中各个属性以及类的的特性和使用。

----

让我们一起共勉：
> 持续不断地学习，是更好的成长 ---TyouSF

----

# 参考资料

----

> [Locust 官网](http://locust.io/)
> [Locust 官方文档](http://docs.locust.io/en/latest/installation.html)
> [Locust 其他参考](http://debugtalk.com/tags/Locust/)
> [Locust Git项目](https://github.com/locustio/locust)
