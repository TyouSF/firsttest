---
title: Python3 bool
date: 2017-05-18 14:18:35
categories:
- Python
tags:
- python
keywords:
---


{% asset_img python.png %}

{% cq %}
--本篇主要讲述 Python数据类型之：布尔型--

“优雅”    “明确”    “简单”
Python
{% endcq %}

<!--more-->


有关布尔型其实相信大家并不陌生，因为这一点我们在上学期间的数学教材中就提到过真与假的相关概念。

在Python中，布尔型的真与假：

- True 表示真
- False 表示假

请注意大小写，这与很多的编程语言中的写法是有一定区别的，请勿混淆。


****

# Python中的布尔

其实关于布尔型的数据，在此并没有太多要说的。

但是我依然相信大多数的初学者对于Python中的 bool 型数据掌握仅仅停留在两个单词 True 和False。

下面我们就来看看一些也许你还并不知道的 bool 型数据。

在 Python 内部，True 和 False 是 bool 的实例，实际上仅仅是内置的整数类型int的子类（以面向对象的观点来看）。

你能够将Ture和False看作是预定义的设置为整数1和整数0的变量。

下面让我们看看在交互式环境中实际的验证：
```
>>> t = True
>>> n = 1
>>> t + 1
2
>>> f = False
>>> n * f
0
```

在上述示例中，我们通过简单的运算可以看到，True 和 False 是可以直接与数字进行运算，并且其值也分别是对应的1和0（从上述例子看起来是这样，其实也确实是这样的，下面让我们更准确的验证：）
```
>>> True == 1
True
>>> False == 0
True
```

我们试图通过Python内部的字面值判断来尝试 `True == 1` 与 `False == 0` 可以看到其结果都得到了True，因此也可以印证 True 与 False 分别对应着 1 和 0。


> 更多关于Bool型，可在 Python 交互式环境下，使用：`help(bool)` 进行查看，或查阅官方文档：[Python 官方文档](https://docs.python.org/3/)。