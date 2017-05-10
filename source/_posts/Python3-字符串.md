---
title: Python3 字符串
date: 2017-04-26 14:22:10
categories:
- Python
tags:
- python
keywords:
---

{% asset_img python.png %}

{% cq %}
--本篇主要讲述 Python数据类型之：字符串--

“优雅”    “明确”    “简单”
Python
{% endcq %}

<!--more-->

Python中的数据类型：字符串。并且**字符串类型不支持原位改变。**
以引号括起来进行书写的字面值在Python中为字符串类型。

Python2中，普通字符串是以8位ASCII码进行存储的，而Unicode字符串则存储为16位unicode字符串，这样能够表示更多的字符集。使用的语法是在字符串前面加上前缀 u 表示 Unicode 字符串。
Python3中，所有的字符串默认都是Unicode字符串。

**相关的方法等示例展示，均以Python的交互式环境演示为主！**

****
# 有关四种不同形式的字符串声明

1. 单引号 （使用单引号保留原字符串内的双引号而无需转换）
```
>>> print('happy "new" year')
happy "new" year
```
2. 双引号 （使用双引号保留原字符串内的单引号而无需转换）
```
>>> print("happy 'new' year")
happy 'new' year
```
3. 三引号 （允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。三引号让程序员从引号和特殊字符串的泥潭里面解脱出来，自始至终保持一小块字符串的格式是所谓的WYSIWYG（所见即所得）格式的。）
```
>>> para_str = """这是一个多行字符串的实例
···多行字符串可以使用制表符
···TAB ( \t )。
···也可以使用换行符 [ \n ]。
···"""
>>> print(para_str)
这是一个多行字符串的实例
多行字符串可以使用制表符
TAB (    )。
也可以使用换行符 [ 
 ]。
```
4. 以 `r` 开头声明的原始字符串 （原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。）
```
>>> path = r'c:\abc\xyz.txt'
>>> path
'c:\\abc\\xyz.txt'
>>> print(path)
c:\abc\xyz.txt
```

****
# Python字符串中的一些特殊字符

使用反斜杠 `\` 转义，常用的转义字符如下表

| 转义字符 |  实际输出结果   |
|   ----   |      ----       |
| `\\`     | `\` 反斜杠符号  |
| `\'`     | `'` 单引号      |
| `\"`     | `"` 双引号      |
| `\n`     | 换行符          |
| `\b`     | 退格(Backspace) |
| `\t`     | 制表符（四空格）|
| `\r`     | 回车            |
| `\a`     | 系统响铃        |

****
# 基本操作

1. `+` 加法操作，字符串连接
```
>>> 'abc' + 'xyz'
'abcxyz'
```

2. `* ` 重复操作，重复输出字符串
```
>>> 'ok' * 5
'okokokokok'
```

3. `len( )` 计算长度
```
>>> len('ok')
2
```

4. `[ ]` 通过索引获取字符串中对应索引处的字符
```
>>> s = 'hello python'
>>> s[0]
'h'
>>> s[-1]
'n'
```

5. `str[x:y:z]` 切片操作（索引由左至右，从0开始）  
x：为切片起始索引  
y：为切片结束索引（结果不包含y索引位置的值）  
z：切片操作的步长
```
>>> s = 'my name is python w'
>>> s[3:7]
'name'
>>> s[-1]
'w'
>>> s[:]
'my name is python w'
>>> s[::2]
'm aei yhnw'
>>> s[::-1]
'w nohtyp si eman ym'
```

6. `ord( )` 与 `chr( )` 字母与数字对应转化
```
>>> ord('c')
99
>>> chr(99)
'c'
```

7. `in` 成员运算符 - 如果字符串中包含给定的字符返回 True
```
>>> s = 'hello python'
>>> 'python' in s
True
```

8. `not in` 成员运算符 - 如果字符串中不包含给定的字符返回 True
```
>>> s = 'hello python'
>>> 'python' not in s
False
```

****
# 字符串类型的常见内建函数

1. `replace( )` 替换字符串 （字符串不支持原位改变，替换后结果需重新赋值给新变量）。
```
>>> s = "hello world"
>>> s.replace('o', 'k')
'hellk wkrld'
```

2. `split()` 以给定字符为分隔符截取字符串，可指定分割次数。分割结果以列表数据类型返回。
```
>>> s = "hello world"
>>> s.split('o')
['hell', ' w', 'rld']
>>> s.split('o',1)
['hell', ' world']
```

3. `capitalize( )` 将字符串首字母转化为大写。
```
>>> s = 'hello world'
>>> s.capitalize()
'Hello world'
```

4. `startswith( )` 判断字符串开始，返回结果为 True 或 False。
```
>>> s = 'hello world'
>>> s.startswith('he')
True
>>> s.startswith('kk')
False
```

5. `endswith( )` 判断字符串结尾，返回结果为 True 或 False。
```
>>> s = 'hello world'
>>> s.endswith('ld')
True
>>> s.endswith('oo')
False
```

6. `count( )` 统计指定字符出现的频率，也可（根据索引）指定统计起止位置。
```
>>> s = 'hello world'
>>> s.count('o')
2
>>> s.count('o', 0, 5)
1
```

7. `find( )` 统计指定字符出现的频率，也可（根据索引）指定查找起止范围。
```
>>> s = 'hello world'
>>> s.count('o')
2
>>> s.count('o', 0, 5)
1
```

8. `format( )` 字符串格式化，使用 format 内传递的内容格式化字符串内指定位置。
```
>>> a = '{} hello python {}'
>>> a.format('abc','xyz')
'abc hello python xyz'
>>> '{}ello {}ython'.format('h', 'p')
'hello python'
```

9. `isalnum( )` 判断字符串是否只包含字母或数字，是则返回 True，否则返回 False。
```
>>> s = 'hello python 3'
>>> s.isalnum()
False
>>> s = 'hellopython3'
>>> s.isalnum()
True
```

10. `isalpha( )` 判断字符串是否只包含字母，是则返回 True，否则返回 False。
```
>>> s = 'hello python 3'
>>> s.isalpha()
False
>>> s = 'hellopython'
>>> s.isalpha()
True
```

11. `isdigit( )` 判断字符串是否只包含数字，是则返回 True，否则返回 False。
```
>>> s = '3.6'
>>> s.isdigit()
False
>>> s = '36'
>>> s.isdigit()
True
```

12. `islower( )` 判断字符串中的所有字母是否为小写，是则返回 True，否则返回 False。
```
>>> s = 'a36a'
>>> s.islower()
True
>>> s = 'a36A'
>>> s.islower()
False
```

13. `isupper( )` 判断字符串中的所有字母是否为大写，是则返回 True，否则返回 False。
```
>>> s = 'A36A'
>>> s.isupper()
True
>>> s = 'A36a'
>>> s.isupper()
False
```

14. `lower( )` 将字符串中的所有字母转换为小写。
```
>>> s = 'HELLO PYTHON 3.6'
>>> s.lower()
'hello python 3.6'
```

15. `upper( )` 将字符串中的所有字母转换为大写。
```
>>> s = 'hello python 3.6'
>>> s.upper()
'HELLO PYTHON 3.6'
```

16. `swapcase( )` 将字符串中的所有字母：大写转换为小写，小写转换为大写。
```
>>> s = 'hello python, HELLO PYTHON'
>>> s.swapcase()
'HELLO PYTHON, hello python'
```

17. `join( )` 以字符串本身作为分隔符，将 join 函数内部迭代器的所有元素进行拼接。
```
>>> s = 'hello'
>>> L = ['Today ', ' python ', ' world']
>>> s.join(L)
'Today hello python hello world'
>>> '.'.join(['www', 'python', 'org'])
'www.python.org'
```

18. `lstrip( )` 去除字符串起始处的空格。
```
>>> s = '  hello python '
>>> s.lstrip()
'hello python '
```

19. `rstrip( )` 去除字符串结尾处的空格。
```
>>> s = '  hello python '
>>> s.rstrip()
'  hello python'
```

20. `strip( )` 去除开头儿和结尾的空格（相当于同时执行了：`lstrip( )` 和 `rstrip( )`）
```
>>> s = '  hello python '
>>> s.strip()
'hello python'
```

> 更多关于字符串数据类型的内建函数方法，可在 Python 交互式环境下，使用：`help(str)` 进行查看，或查阅官方文档：[Python 官方文档](https://docs.python.org/3/)。