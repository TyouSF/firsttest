---
title: Python3 文件（上）
date: 2017-05-12 10:39:46
categories:
- Python
tags:
- python
keywords:
---

{% asset_img python.png %}

{% cq %}
--本篇主要讲述 Python数据类型之：文件--

“优雅”    “明确”    “简单”
Python
{% endcq %}

<!-- more -->

说起文件，很多人可能并不认为这应当是一个数据类型，其实在Python当中：
一切皆对象。而且在Python当中，文件的读写都是通过文件对象：file，来完成的。
尽管将文件归为数据类型不太确切，但我们并不纠结于此，目的在于如何灵活的掌握和使用Python来完成对我们日常文件的管理需求。

在Python3中，文件默认会以UTF-8的编码进行读写。

文件都有很多类型，诸如：txt，excel，csv等。并且不同的文件类型，在读取和操作方面都有些各自的方法和特点，所以关于文件的讲解，分为上篇和下篇。本文为上篇，主要基于基本的文件类型：txt来进行，有关excel、csv等的讲解请看下篇，传送门：

{% post_link "Python3-文件（下）" %}


****
# 文件 File 对象的创建

1. 基本的形式：
```
file = open('file', "mode")
```

r w a 是三种最基本的模式：  
- r (read) 读取
- W (write) 写入
- a (append) 追加

更多 mode 参数所对应的值如下表：

| 模式 | 含义                                                            |
| ---- | ----                                                            |
| r    | 以只读方式打开文件。文件指针指向文件开头，从头读取。（默认模式）|
| rb   | 以二进制格式打开一个文件用于只读。                              |
| r+   | 打开一个文件用于读写                                            |
| rb+  | 以二进制格式打开一个文件用于读写                                |
| w    | 只用于写入。文件存在则覆盖写入。文件不存在，则创建并写入        |
| w+   | 打开一个文件用于读写                                            |
| wb+  | 以二进制格式打开一个文件用于读写                                |
| a    | 追加模式，文件存在，文件指针指向文件结尾，从内容末尾开始写入    |
| ab   | 二进制格式打开一个文件用于追加                                  |
| a+   | 打开一个文件用于读写，存在的文件进行追加，不存在则创建新文件    |
| ab+  | 二进制格式打开一个文件用于追加                                  |


 
****
# 文件 File 对象的基本操作

** 值得注意的是：**  
所有文件对象操作的最后，都要对文件进行关闭，来结束所有操作并保存最终的结果；以避免下一次操作时发生冲突或者其他问题的产生。


****
# 文件 File 对象的部分属性

1. `name` 可以获取到当前文件对象的文件名
```
>>> f = open("testfile.txt", "r")
>>> f.name
'testfile.txt'
```

2. `mode` 当前文件的模式
```
>>> f = open("testfile.txt", "r")
>>> f.mode
'r'
```

3. `closed` 文件关闭状态，关闭为 True
```
>>> f = open("testfile.txt", "r")
>>> f.closed
False
>>> f.close()
>>> f.closed
True
```


****
# 基本操作

1. 基本的写入：
```
>>> f = open("testfile.txt", "w")
>>> f.write("我写的第一行数据")
8
>>> f.close()
```

2. `read("size")` 从文件读取指定的字节数，如果未给定或为负则读取所有：
```
>>> f = open("testfile.txt", "r")
>>> f.read()
'我写的第一行数据'
>>> f.close()
>>> f = open("testfile.txt", "r")
>>> f.read(1)
'我'
>>> f.read(2)
'写的'
>>> f.close()
```

3. `readline("size")` 逐行读取，包括 "\n" 字符，size指定读取当前行的字节数。
```
>>> f = open("testfile.txt", "r")
>>> f.readline()
'我写的第一行数据\n'
>>> f.readline()
'第二行数据\n'
>>> f.readline()
'第三行数据\n'
>>> f.close()
>>> f = open("testfile.txt", "r")
>>> f.readline(1000)
'我写的第一行数据\n'
```

4. `readlines()` 读取所有行并返回列表，若给定sizeint>0，返回总和大约为sizeint字节的行, 实际读取值可能比 sizeint 较大, 因为需要填充缓冲区。
```
>>> f = open("testfile.txt", "r")
>>> f.readlines()
['我写的第一行数据\n', '第二行数据\n', '第三行数据\n']
>>> f.close()
>>> f = open("testfile.txt", "r")
>>> f.readlines(10)
['我写的第一行数据\n', '第二行数据\n']
>>> f.close()
```

5. `tell()` 返回当前文件指针位置
```
>>> f = open("testfile.txt", "r")
>>> f.tell()
0
>>> f.readline()
'第一行\n'
>>> f.tell()
8
```

6. `readable()` 查看文件是否以读取模式打开，是则为True
```
>>> f = open("testfile.txt", "r")
>>> f.readable()
True
>>> f.close()
>>> f = open("testfile.txt", "w")
>>> f.readable()
False
>>> f.close()
```

7. `seek(cookie, whence=0, /)` 按照给定的参考位置，重新调整指针的位置，whence可设定的数值为：0（默认值，以文件开头开始），1（当前指针位置开始），2（文件末尾处开始，此时cookie偏移数是不支持设定的，可以设定为0）
```
>>> f = open("testfile.txt", "r")
>>> f.tell()
0
>>> f.readline()
'第一行\n'
>>> f.tell()
8
>>> f.seek(0,0)
0
>>> f.readline()
'第一行\n'
>>> f.seek(0,2)
22
>>> f.readline()
''
>>> f.close()
```

****
# 二进制文件

二进制文件在Python中，配合pickle，更适合进行一些Python对象的存储。

一个完整读写，通常类似这样：
```
>>> f = open("testfile.pkl", "wb")
>>> d = {"a":1, "b":2}
>>> import pickle
>>> pickle.dump(d, f)
>>> f.close()
>>> f = open("testfile.pkl", "rb")
>>> data = pickle.load(f)
>>> data
{'a': 1, 'b': 2}
```


****
# 文件操作的注意事项

每次对文件对象的操作结束后，将文件关闭是一个良好的编码习惯，也是最为安全和必要的行为；
每次对文件对象的操作结束后，将文件关闭是一个良好的编码习惯，也是最为安全和必要的行为；
每次对文件对象的操作结束后，将文件关闭是一个良好的编码习惯，也是最为安全和必要的行为；

有一种更为简便的方式可以更快捷的完成对文件的操作并且可以不用担心文件没有被关闭，那便是上下文操作，使用 with 语句，通常像是这样的使用：
```
>>> with open("testfile.txt", "r") as f:
...     for line in f.readlines():
...             print(line)
...
第一行

第二行

第三行
```


> 更多关于文件对象的操作，可查阅官方文档：[Python 官方文档](https://docs.python.org/3/)。