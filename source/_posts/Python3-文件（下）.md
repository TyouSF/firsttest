---
title: Python3 文件（下）
date: 2017-05-14 10:39:46
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

如果对文件基础部分的了解和操作还不清楚，可以查看文件（上）篇，传送门：
{% post_link "Python3-文件（上）" %}


本章将主要介绍在Python中：
如何对 CSV、Excel 文件进行读写的相关操作。


****
# CSV 文件

CSV：C表示逗号，S表示分隔，V表示值，通俗的来说CSV即“逗号分隔值”。
通常将数据库中存储的数据，以csv文件的形式来导出进行数据上的一些管理和交换等。

**值得注意的是：**
有关csv文件的打开和阅读建议使用专门的csv文件阅读器，可自行搜索。非常不建议也不支持使用某软家的excel来进行管理，容易造成一些你意想不到的问题和麻烦，请慎重考虑。


## CSV 文件读取

有关csv文件操作，在Python内部已有相关模块集成，无需再安装，可以直接使用。
通常这样导入：
```
import csv
```

假定我们实现存储好这样一个CSV文件，文件名为：“testcsv.csv”，形如：
```
id,name,price,publictime
1,第01行,10$,2100-10-10
2,第02行,11$,2100-10-11
3,第03行,12$,2100-10-12
4,第04行,13$,2100-10-13
5,第05行,14$,2100-10-14
```

我们的读取过程通常会是像这样的：
```
>>> import csv
>>> f = open("testcsv.csv", encoding="utf-8")
>>> f_csv = csv.reader(f)
>>> next(f_csv)
['id', 'name', 'price', 'publictime']
>>> f.close()
```

解释：
在CSV文件读取时，通常先创建一个文件对象，在上例中，我们的文件对象是 f，之后再使用csv模块的 reader() 函数来加载csv的文件对象 f，这样便拥有了一个csv文件操作的容器，本例是 f_csv。

1. csv的reader对象支持遍历：
```
>>> f = open("testcsv.csv", encoding="utf-8")
>>> f_csv = csv.reader(f)
>>> f_csv
<_csv.reader object at 0x000001A7084B83F0>
>>> for row in f_csv:
...     print(row)
...
['id', 'name', 'price', 'publictime']
['1', '第01行', '10$', '2100-10-10']
['2', '第02行', '11$', '2100-10-11']
['3', '第03行', '12$', '2100-10-12']
['4', '第04行', '13$', '2100-10-13']
['5', '第05行', '14$', '2100-10-14']
>>> f.close()
```

2. 以字典表的方式读取
```
>>> f = open("testcsv.csv", encoding="utf-8")
>>> f_csv = csv.DictReader(f)
>>> for row in f_csv:
...     print(row)
...
OrderedDict([('id', '1'), ('name', '第01行'), ('price', '10$'), ('publictime', '2100-10-10')])
OrderedDict([('id', '2'), ('name', '第02行'), ('price', '11$'), ('publictime', '2100-10-11')])
OrderedDict([('id', '3'), ('name', '第03行'), ('price', '12$'), ('publictime', '2100-10-12')])
OrderedDict([('id', '4'), ('name', '第04行'), ('price', '13$'), ('publictime', '2100-10-13')])
OrderedDict([('id', '5'), ('name', '第05行'), ('price', '14$'), ('publictime', '2100-10-14')])
>>> f.close()
```

## CSV 文件写入

假定我们要使用Python完成如下的一个csv文件内容的写入，内容如下：
```
id,name
1,第01行
2,第02行
```

### 以元组的形式实现写入：

```
>>> import csv
>>> csv_header = ["id", "name"]
>>> csv_row = [
... (1, "第01行"),
... (2, "第02行")
... ]
>>> with open("writecsv.csv", "w", encoding="utf8", newline="") as f:
...     write_csv = csv.writer(f)
...     write_csv.writerow(csv_header)
...     write_csv.writerows(csv_row)
...
9
>>> with open("writecsv.csv", "r", encoding="utf8") as f:
...     reader = csv.reader(f)
...     for row in reader:
...             print(row)
...
['id', 'name']
['1', '第01行']
['2', '第02行']
```

### 以字典表的形式实现写入：

```
>>> import csv
>>> csv_header = ["id", "name"]
>>> csv_row = [{"id":1, "name":"第01行"}, {"id":2, "name":"第02行"}]
>>> with open("dictwritecsv.csv", "w", encoding="utf8", newline="") as f:
...     csv_write = csv.DictWriter(f, csv_header)
...     csv_write.writeheader()
...     csv_write.writerows(csv_row)
...
>>> with open("dictwritecsv.csv", "r", encoding="utf8") as f:
...     reader = csv.reader(f)
...     for row in reader:
...             print(row)
...
['id', 'name']
['1', '第01行']
['2', '第02行']
```

 
****
# Excel 文件

有关 Excel 文件的读写和操作，Python内部并没有直接可以使用的方法，需要借助额外的包：
- `xlrd` 用于读取 Excel 文件
- `xlwt` 用于写入 Excel 文件

安装可以使用：
```
>>> pip install xlrd
>>> pip install xlwt
```

**注明：**本篇将主讲解 xlrd 的读取相关的操作，有关 xlwt 的写入可查看相关资料。

## xlrd 的使用

通常我们的读取会像这样：
```
import xlrd


def xl_read():
    """Excel 文件读取"""

    book = xlrd.open_workbook("testexcel.xlsx")
    sheet = book.sheet_by_index(0)
    sheet_name = sheet.name  # 可获取当前工作表的名称
    sheet_rows = sheet.nrows  # 可获取当前工作表的总行数

    for row_index in range(sheet.nrows):
        print(sheet.row_values(row_index))  # 打印索引指定行的数据
```

**相关解释：**

1. 使用 xlrd 读取 excel 文件，基本方法需要使用 `open_workbook("excelfilename")` 构建基本的读取器，这里我们定义为 book

2. `book` 读取器建立后，要进一步指定我们所需要读取的是哪一张工作表的数据（众所周知excel文件内可以包含多个工作表，英文叫 sheet），而 `book` 为我们提供两种方法：
	- sheet_by_name() 通过工作表的名称来指定
	- sheet_by_index() 通过工作表的索引来指定，默认从0开始

3. 在上一步中，我们通过 `sheet_by_index()` 来创建了 sheet 对象，通过 sheet 对象，我们可以获取到一些基本的属性：
	- name 当前读取表的表名
	- nrows 当前读取表有效数据的总行数

4. 有了 sheet 对象，我们便可以通过 `sheet.row_values()` 来获取指定行的数据：
	- `sheet.row_values()` 接受行的索引作为参数查询指定行的数据


**一些需要说明的：**
xlrd 所读取的 excel 中每一行的数据，其返回的都是将该行每一个单元格内的数据转化为字符串，并以列表的形式返回。更为详细的可自行进行尝试打印来获取更准确的信息。


> 更多关于文件对象的操作，可查阅官方文档：[Python 官方文档](https://docs.python.org/3/)。