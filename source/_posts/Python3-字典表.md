---
title: Python3 字典表
date: 2017-05-10 15:16:36
categories:
- Python
tags:
- python
keywords:
---

{% asset_img python.png %}

{% cq %}
--本篇主要讲述 Python数据类型之：字典表--

“优雅”    “明确”    “简单”
Python
{% endcq %}

<!--more-->

Python中的数据类型：字典表。并且**字典表数据类型支持原位改变**。
字典表内的每一个元素，都是以键值（key=>value）对的形式组成，键值对用冒号(:)分割，每个元素之间用逗号（,）分割，整个字典包括在花括号（{}）中 ,格式如下所示：
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> type(d)
<class 'dict'>
```

注意：
字典表的键必须是唯一的，但值则不必。
值可以取任何数据类型，但键必须是不可变的，如字符串，数字或元组。

****
# 字典表的声明

1. 使用基本的形式进行定义：
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> type(d)
<class 'dict'>
```

2. 使用 `dict( )` 进行声明：
```
>>> d = dict(name='python', verison='3.6')
>>> d
{'name': 'python', 'verison': '3.6'}
>>> type(d)
<class 'dict'>
```

****
# 字典表的基本访问

1. 基本访问形式，类似索引的方式，但是字典表使用的是[key]的形式来访问：
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> d['key1']
'value1'
>>> d['key3']
'value3'
```

2. 使用字典表的内置方法：`dit.get( )`：
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> d.get('key1')
'value1'
>>> d.get('key2')
'value2'
```

> 二者访问的区别：
第一种方式，访问不存在的键时，会直接报错；
第二种方式可以避免在访问不存在的键时发生的错误，并且可以给出未找到时的默认返回内容。
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> d['key4']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'key4'
>>> d.get('key4', '未找到该元素')
'未找到该元素'
```

****
# 字典表的修改与添加

1. 修改字典表内已有的元素：
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> d['key1'] = '我修改了key1的值'
>>> d
{'key1': '我修改了key1的值', 'key2': 'value2', 'key3': 'value3'}
```

2. 通过基本的赋值（字典表内没有的键）来增加元素：
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> d['add'] = 'success'
>>> d
{'key1': 'value1', 'key2': 'value2', 'key3': 'value3', 'add': 'success'}
```

****
# 基本操作

1. `len( )` 计算字典表的元素个数：
```
>>> d = {'key1':'value1', 'key2':'value2', 'key3':'value3'}
>>> len(d)
3
>>
```

2. 字典表内置函数 `clear( )` 删除字典表内所有元素：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> d
{'a': 1, 'b': 2, 'c': 3}
>>> d.clear()
>>> d
{}
```

3. 字典表内置函数 `copy( )` 复制并返回字典表内所有元素：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> d.copy()
{'a': 1, 'b': 2, 'c': 3}
```

4. 字典表内置函数 `fromkeys( )` 根据指定的可迭代对象创建含有初始值的字典表：
```
>>> d = {}
>>> fk = ('x', 'y', 'z')
>>> d.fromkeys(fk, 0)
{'x': 0, 'y': 0, 'z': 0}
>>> d
{}
>>> newd = d.fromkeys(fk, 0)
>>> newd
{'x': 0, 'y': 0, 'z': 0}
```

5. 字典表内置函数 `get( )` 获取字典表内某键的值：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> d.get('a')
1
>>> result = d.get('d')
>>> result
>>> type(result)
<class 'NoneType'>
>>> d.get('d', 'noresult')
'noresult'
```

6. 字典表内置函数 `items( )` 返回可遍历的(键, 值) 元组数组：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> d.items()
dict_items([('a', 1), ('b', 2), ('c', 3)])
```

7. 字典表内置函数 `keys( )` 返回一个字典所有的键：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> d.keys()
dict_keys(['a', 'b', 'c'])
```

8. 字典表内置函数 `pop( )` 删除字典表内的指定元素并返回键对应的值，同时可指定异常时的返回内容：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> d.pop('a')
1
>>> d.pop('e')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'e'
>>> d.pop('e', '未找到')
'未找到'
```

9. 字典表内置函数 `update( )` 把字典dict2的键/值对更新到dict里：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> newd = {'x':4}
>>> d.update(newd)
>>> d
{'a': 1, 'b': 2, 'c': 3, 'x': 4}
```

10. 字典表内置函数 `values( )` 返回字典中的所有值：
```
>>> d = {'a':1, 'b':2, 'c':3}
>>> d.values()
dict_values([1, 2, 3])
```

> 更多关于字典表数据类型的内建函数方法，可在 Python 交互式环境下，使用：`help(dict)` 进行查看，或查阅官方文档：[Python 官方文档](https://docs.python.org/3/)。