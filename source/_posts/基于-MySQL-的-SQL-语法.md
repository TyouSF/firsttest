---
title: 基于 MySQL 的 SQL 语法
date: 2017-08-10T10:33:47.000Z
categories:
  - 数据库
tags:
  - MySQL
keywords:
---

{% asset_img mysql.png %}

{% cq %} 数据库，简单来说可视为电子化的文件柜----存储电子文件的处所，用户可以对文件中的数据运行新增、截取、更新、删除等操作。 数据库指的是以一定方式储存在一起、能为多个用户共享、具有尽可能小的冗余度、与应用程序彼此独立的数据集合。

维基百科 {% endcq %}

本篇旨在基于 MySQL 为基础的数据库，探讨和学习基本关系型数据库的一些 SQL 语法。

不涉及数据库类型以及其他数据库的差异研究。

<!-- more -->

----

 # MySQL 安装

有关 MySQL 的安装这里不在多说，网上的安装教程也都很全。

大家可自行百度，根据自己当前使用的操作系统进行安装。

由于 mac 的环境变量设置相对 winddows 有些不同，这里简单记录下。

## Mac 上的安装

**前提**： 如果安装 Myql 使用的是官方下载的 dmg 文件包方式安装的，那么安装后可能存在 mysq 命令无效。

此时就需要对 mac 进行相关的环境变量的配置了。

### 了解 Mac 的环境变量

Mac 在加载环境变量是，有以下的顺序（优先级从上到下）↓：

```
/etc/profile
/etc/paths
~/.bash_profile
~/.bash_login
~/.profile
~/.bashrc
```

**备注**： `/etc/profile` 和 `/etc/paths` 是系统级别的，系统启动就会加载， 后面几个是当前用户级的环境变量。

其次根据当前 `shel` 的类型，如果是 `bash` 则启动加载 `.bashrc` 的环境变量，如果是<br>
`zsh` 则加载的便是 `.zshrc` 文件中的环境变量

最后便是在对应的环境变量文件中添加 mysql 的环境变量，添加语句如下：

```
export PATH=${PATH}:/usr/local/mysql/bin
```

**说明**：如果是默认安装的话

----

# MySQL 基本语句

我们讲解语句的顺序是基于从无到有再到使用再到无的过程，按照这样的顺序  
可以更快的学习到 MySQL 的整个使用过程和数据库的生命周期。

## 启动 MySQL

在不同的操作系统上启动 MySQL 的服务

## 连接 MySQL

```
mysql -uroot -ppassword
```

连接解释：

* `-u` 后面跟随连接数据库的用户名，一般默认的是 root
* `-p` 后面跟随当前连接数据库用户的密码，有的时候在安装时有默认密码，有的为空
* `-p` 可以后面不直接跟密码，输入 `-p` 后直接回车，会在新行输入密码，此时密码并不可见

## 创建数据库

```
CREATE DATABASE IF NOT EXISTS databasename;
```

* `IF NOT EXISTS` 是可选项，表示只有在不存在当前创建的数据库时进行创建，可避免报错

## 显示数据库

```
SHOW DATABASES;
```

## 选择数据库

```
USE databasename;
```

## 删除数据库

```
DROP DATABASE IF EXISTS databasename;
```

* `IF EXISTS` 可选项，只有在存在要删除的数据库才删除

## 创建表

数据库是表的容器，表存在于数据库中。

创建表前，先要连接选择对应的数据库，方可创建。

```
CREATE TABLE IF NOT EXISTS tablename (
    column_name data_type[size] [NOT NULL|NULL] [DEFAULT value] [AUTO_INCREMENT],
    column_name data_type[size] [NOT NULL|NULL] [DEFAULT value] [AUTO_INCREMENT],
    column_name data_type[size] [NOT NULL|NULL] [DEFAULT value] [AUTO_INCREMENT],
    ...
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

示例：
```
CREATE TABLE `orderdetails` (
  `orderNumber` int(11) NOT NULL,
  `productCode` varchar(15) NOT NULL,
  `quantityOrdered` int(11) NOT NULL,
  `priceEach` decimal(10,2) NOT NULL,
  `orderLineNumber` smallint(6) NOT NULL,
  PRIMARY KEY (`orderNumber`,`productCode`),
  KEY `productCode` (`productCode`),
  CONSTRAINT `orderdetails_ibfk_1` FOREIGN KEY (`orderNumber`) REFERENCES `orders` (`orderNumber`),
  CONSTRAINT `orderdetails_ibfk_2` FOREIGN KEY (`productCode`) REFERENCES `products` (`productCode`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

## 添加数据（插入数据）

```
INSERT INTO tablename (column1,column2...)
VALUES (value1,value2,...);
```

## 查询数据

```
SELECT
    column_1, column_2, ...
FROM
    table_1
[INNER | LEFT |RIGHT] JOIN table_2 ON conditions
WHERE
    conditions
GROUP BY column_1
HAVING group_conditions
ORDER BY column_1
LIMIT offset, length;
```

## 条件

```
SELECT
    lastname, firstname, jobtitle
FROM
    employees
WHERE
    jobtitle = 'Sales Rep';
```

## 更新数据

```
UPDATE [LOW_PRIORITY] [IGNORE] table_name
SET
    column_name1 = expr1,
    column_name2 = expr2,
    ...
WHERE
    condition;
```

## 删除表数据

```
DELETE FROM employees
WHERE
    officeCode = 4;
```

使用 limit 删除：

```
DELETE FROM customers
WHERE country = 'France'
ORDER BY creditLimit
LIMIT 5;
```

## 修改表结构

```
ALTER TABLE table_name action1[,action2,…];
```

示例：

1. 添加新列
```
ALTER TABLE tasks
ADD COLUMN complete DECIMAL(2,1) NULL
AFTER description;
```

2. 删除列
```
ALTER TABLE tasks
DROP COLUMN description;
```

3. 重命名表
```
ALTER TABLE tasks
RENAME TO work_items;
```

## 重命名表

```
RENAME TABLE old_table_name TO new_table_name;
```

----

让我们一起共勉：
> 持续不断地学习，是更好的成长 ---TyouSF

----

# 参考资料

----

> [MySQL 官网](https://www.mysql.com/)
> [MySQL 易百教程](http://www.yiibai.com/mysql/)
> [MySQL 菜鸟教程](http://www.runoob.com/mysql/mysql-tutorial.html)
