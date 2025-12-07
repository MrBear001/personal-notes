# MySQL

---

## 一、MySQL 概述

软件的核心是数据，数据如何存储？答案是数据库（DataBase，DB）。数据库是专门用来存储和管理数据的地方。

而 MySQL 则是一款数据库管理系统（DataBase Manage System，DBMS），通过它可以便捷地存储和管理数据。

与 MySQL 交互需要通过一门结构化查询语言（Stuctured Query Languge）来实现，也就是 SQL。如何编写 SQL 使我们学习的重点。

## 二、SQL

### 1. SQL 的分类

SQL 根据其作用不同，可以分为以下四类：

* DDL —— 数据定义语言 —— 用来定义数据库对象（数据库、表、字段）
* DML —— 数据操作语言 —— 用来对表中的数据进行增删改操作
* DQL —— 数据查询语言 —— 用来对表中的数据进行查询操作
* DCL —— 数据控制语言 —— 用来创建数据库用户和控制数据库的访问权限

### 2. DDL

库定义：

```sql
# 查询所有数据库
SHOW DATABASES;
# 创建数据库
CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
# 查询建库语句
SHOW CREATE DATABASE 数据库名;
# 使用/切换数据库
USE 数据库名;
# 查询当前使用的数据库
SELECT DATABASE();
# 删除数据库
DROP DATABASE [IF EXISTS] 数据库名;
```

表定义：

```sql
# 查询当前库中的所有表
SHOW TABLES;
# 创建表
CREATE TABLE [IF NOT EXISTS] 表名 (
	字段1 类型 [约束] [COMMENT 注释],
	字段2 类型 [约束] [COMMENT 注释],
	...
    [表级约束]
) [ENGINE=存储引擎] [DEFAULT CHARSET=字符集] [COLLATE=排序规则] [COMMENT 注释];
# 查看表结构
DESC 表名;
# 查询建表语句
SHOW CREATE TABLE 表名;
# 修改表
ALTER TABLE 表名 ADD 字段名 类型 [约束] [COMMENT 注释]; # 添加字段
ALTER TABLE 表名 CHANGE 字段名 新字段名 类型 [约束] [COMMENT 注释]; # 修改字段
ALTER TABLE 表名 DROP 字段名; # 删除字段
ALTER TABLE 表名 RENAME TO 新表名; # 重命名表
# 删除表
DROP TABLE [IF EXISTS] 表名;
```







## 三、MySQL 的数据类型

我们在建表时需要指定每个字段的数据类型以提高存储效率和节约存储空间。MySQL 中主要提供了数值、字符串和日期时间这三类数据类型。

### 1. 数值类型

整数：

* TINYINT
* SMALLINT
* MEDIUMINT
* INT
* BIGINT

所有的整数类型都可以添加 UNSIGNED 关键字，表示无符号整数，这样可以将正数的存储范围扩大一倍。

浮点数：

* FLOAT
* DOUBLE
* DECIMAL

### 2. 字符串类型

短字符串：

* CHAR
* VACHAR

长文本：

* TINYTEXT
* TEXT
* MEDIUMTEXT
* LONGTEXT

### 3. 日期时间类型

* DATE
* TIME
* YEAR
* DATETIME
* TIMESTAMP
