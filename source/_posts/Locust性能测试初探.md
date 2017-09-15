---
title: Locust性能测试初探
date: 2017-08-04T16:57:00.000Z
categories:
  - Locust
tags:
  - python
  - locust
  - 性能测试
keywords: null
---

{% asset_img locust.png %}

{% cq %} An open source load testing tool.

Define user behaviour with Python code, and swarm your system with millions of simultaneous users.

--Locust {% endcq %}

<!-- more -->

 写在开始前：

本文的有关教程，更多的也是搬砖（都来自官网的教程文档），所以，如果各位看官英文功力深厚，可略，直接阅读官网文档。 当然，本文也会在文中提到一些部分或许有用的实际场景，帮助大家更快的上手。

--------------------------------------------------------------------------------

# 性能测试

--------------------------------------------------------------------------------

关于性能测试的介绍，百度或者 google 网上有的是介绍的文章，此处摘录百度部分介绍：

性能测试是通过自动化的测试工具模拟多种正常、峰值以及异常负载条件来对系统的各项性能指标进行测试。负载测试和压力测试都属于性能测试，两者可以结合进行。通过负载测试，确定在各种工作负载下系统的性能，目标是测试当负载逐渐增加时，系统各项性能指标的变化情况。压力测试是通过确定一个系统的瓶颈或者不能接受的性能点，来获得系统能提供的最大服务级别的测试。

有关性能测试的一些理论知识等，此处不再一一讲解，本文将主要介绍 locust 性能测试框架的一些使用。

--------------------------------------------------------------------------------

# Locust 简介

--------------------------------------------------------------------------------

官方对 locust 是这样说的：

"A modern load testing framework" --一款当代的压力测试框架

因此，Locust 是一款集易用、可分布式的压力测试工具，并且具有方便配置与观察的 web 页面。

基本特性：

- Python 语言编写压测场景
- 支持单机或多台分布式压测
- Web UI
- 能够测试多种系统
- 协程

--------------------------------------------------------------------------------

# Locust 安装

--------------------------------------------------------------------------------

使用基本的 pip 命令来安装：

- `pip install locustio`
- `pip install pyzmq`

安装后使用：`locust --help` 来检测是否成功。

如果遇到问题，也可去 locust 的 Git 项目地址中去查看，通常情况下我们所遇到的问题，别人都已经遇到过，并且已经有解决方案了。

--------------------------------------------------------------------------------

# 简单的示例

--------------------------------------------------------------------------------

```python
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

以上的代码所做的事情：

1. 函数定义了所需要压测或者访问的行为
2. UserBehavior 类定义了用户行为的集合（所有的行为来自于函数的定义）
3. WebsiteUser 模拟压测场景的用户对象，压测时，产生的压力用户就来自于 WebsiteUser 对象类

另一种可能的形式是：

```python
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

--------------------------------------------------------------------------------

# 启动 locust

--------------------------------------------------------------------------------

我们将简单示例中的代码保存在名为 "locustfile.py" 的文件中，然后在命令行中执行：

```
locust --host=http://example.com
```

locustfile.py 文件是 locust 框架默认的脚本名，如果脚本名称不是这个，则需要在执行的时候，通过`-f`参数来指定文件即可。

成功运行后，打开浏览器，访问地址：`http://127.0.0.1:8089` 即可打开 locust 的 webUI 界面，如下： {% asset_img locust01.png %}

在界面中我们需要配置两个参数：

- Number of users to simulate：模拟的用户数，即压测的用户总数
- Hatch rate：压测时，每秒并发/启动的用户数

我们配置后，就可以进入到压测的监控页面，可以看到实时的性能测试结果，以及访问接口的情况。

--------------------------------------------------------------------------------

# 最后

--------------------------------------------------------------------------------

当前只是讲解了基本的示例和快速启动，接下来，将在后续的文章中不定时更新具体实例与一些用法的介绍，欢迎关注。

--------------------------------------------------------------------------------

让我们一起共勉：

> 持续不断地学习，是更好的成长 ---TyouSF

--------------------------------------------------------------------------------

# 参考资料

--------------------------------------------------------------------------------

> [Locust 官网](http://locust.io/)

> [Locust 文档](http://docs.locust.io/en/latest/)

> [Locust 项目地址](https://github.com/locustio/locust)
