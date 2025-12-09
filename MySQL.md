# MySQL

---

## 一、MySQL 概述

软件的核心是数据，数据如何存储？答案是数据库（DataBase，DB）。数据库是专门用来存储和管理数据的地方。

而 MySQL 则是一款数据库管理系统（DataBase Manage System，DBMS），通过它可以便捷地存储和管理数据。

与 MySQL 交互需要通过一门结构化查询语言（Stuctured Query Languge）来实现，也就是 SQL。如何编写 SQL 是我们学习的重点。

## 二、SQL 基础

SQL 是结构化查询语言，是一种专门操作关系型数据库的语言。SQL 有统一的标准，不同的数据库厂商都遵循这个标准，但是又各自有不同的扩展，所以 SQL 是有方言存在的。在学习 MySQL 时，要重点学习标准的 SQL 写法，同时也要了解 MySQL 特有的 SQL 方言。

### 1、SQL 的分类

SQL 根据其作用不同，可以分为以下四类：

* DDL —— 数据定义语言 —— 用来定义数据库对象
* DML —— 数据操作语言 —— 用来对表中的数据进行增删改操作
* DQL —— 数据查询语言 —— 用来对表中的数据进行查询操作
* DCL —— 数据控制语言 —— 用来管理数据库的用户及其权限

### 2、DDL

DDL 语句中有与库定义相关的，还有与表定义相关的。

1）库定义相关的语句：

```sql
-- 查询所有数据库
SHOW DATABASES;
-- 创建数据库
CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
-- 查询建库语句
SHOW CREATE DATABASE 数据库名;
-- 使用/切换数据库
USE 数据库名;
-- 查询当前使用的数据库
SELECT DATABASE();
-- 删除数据库
DROP DATABASE [IF EXISTS] 数据库名;
```

2）表定义相关的语句：

```sql
-- 查询当前库中的所有表
SHOW TABLES;
-- 创建表
CREATE TABLE [IF NOT EXISTS] 表名 (
	字段1 类型 [约束] [COMMENT 注释],
	字段2 类型 [约束] [COMMENT 注释],
	...
    [表级约束]
) [ENGINE=存储引擎] [DEFAULT CHARSET=字符集] [COLLATE=排序规则] [COMMENT 注释];
-- 查看表结构
DESC 表名;
-- 查询建表语句
SHOW CREATE TABLE 表名;
-- 修改表
ALTER TABLE 表名 ADD 字段名 类型 [约束] [COMMENT 注释]; -- 添加字段
ALTER TABLE 表名 CHANGE 字段名 新字段名 类型 [约束] [COMMENT 注释]; -- 修改字段
ALTER TABLE 表名 DROP 字段名; -- 删除字段
ALTER TABLE 表名 RENAME TO 新表名; -- 重命名表
-- 删除表
DROP TABLE [IF EXISTS] 表名;
```

### 3、DML

```sql
-- 新增操作
INSERT INTO 表名 VALUES (值1, 值2, ...); -- 新增时指定所有字段
INSERT INTO 表名 (字段1, 字段2, ...) VALUES (值1, 值2, ...); -- 新增时指定部分字段
INSERT INTO 表名 VALUES (值1, 值2, ...), (值1, 值2, ...), ...; -- 批量新增
INSERT INTO 表名 (字段1, 字段2, ...) VALUES (值1, 值2, ...), (值1, 值2, ...), ...;
-- 更新操作
UPDATE 表名 SET 字段1 = 值1, 字段2 = 值2, ... [WHERE 条件];
-- 删除操作
DELETE FROM 表名 [WHERE 条件];
```

### 4、DQL

DQL 语句是比较复杂的，而且在查询时还分为单表查询和多表查询。我们可以先通过单表查询熟悉 DQL 语句的基本用法，然后再拓展到多表查询。

1）单表查询：

一个比较完整的单表查询的 DQL 语句大概长这样：

```sql
SELECT [DISTINCT] * | 字段1 [AS 别名], 字段2 [AS 别名], ... -- 加DISTINCT表示去重，加AS表示取别名，AS可以省略
FROM 表名 [AS 别名]
[WHERE 条件]
[GROUP BY 字段]
[HAVING 分组后条件]
[ORDER BY 字段 [ASC | DESC]] -- ASC表示升序排序，DESC表示降序排序，默认就是ASC，也可以指定多个排序字段
[LIMIT [起始索引], 查询数量];
```

它的执行顺序为：FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY -> LIMIT

2）多表查询：

多表查询是指同时从多张表中查询数据，它有以下几种形式：

```sql
-- 内连接（只返回两个表中满足连接条件的记录）
SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件;
SELECT 字段列表 FROM 表1, 表2 WHERE 连接条件; -- 隐式的内连接写法
-- 左外连接（返回左表中所有的记录和右表中满足连接条件的记录，右表没有匹配的用 NULL 填充）
SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 连接条件;
-- 右外连接（返回右表中所有的记录和左表中满足连接条件的记录，左表没有匹配的用 NULL 填充，右外连接可以改写成左外连接）
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 连接条件;
-- 全外连接（MySQL 不支持 FULL OUTER JOIN 全外连接，但可通过 UNION 模拟）
```

## 三、MySQL 的数据类型

我们在建表时需要指定每个字段的数据类型以提高存储效率和节约存储空间。MySQL 中主要提供了数值、字符串和日期时间这三类数据类型。

### 1、数值类型

整数：TINYINT、SMALLINT、MEDIUMINT、INT、BIGINT

所有的整数类型都可以添加 UNSIGNED 关键字，表示无符号整数，这样可以将正数的存储范围扩大一倍。

浮点数：FLOAT、DOUBLE、DECIMAL

### 2、字符串类型

短字符串：CHAR、VARCHAR

长文本：TINYTEXT、TEXT、MEDIUMTEXT、LONGTEXT

### 3、日期时间类型

DATE、TIME、YEAR、DATETIME、TIMESTAMP

## 四、MySQL 的函数

Excel 表格提供有大量的函数便于我们进行统计计算，而 MySQL 也提供了大量内置函数，用于处理字符串、数值、日期时间、聚合操作等，常见的函数如下。

### 1、字符串函数

```sql
# CONCAT 连接字符串
SELECT CONCAT('Hello', ' ', 'World'); # 'Hello World'
# TRIM 去除字符串首尾的空格
SELECT TRIM('  hello  '); # 'hello'
```

### 2、数值函数

```sql
# ABS 取绝对值
SELECT ABS(-10); # 10
# ROUND 四舍五入保留几位小数
SELECT ROUND(123.456, 2); # 123.46
```

### 3、日期时间函数

```sql
# NOW 返回当前时间
SELECT NOW(); # 如 '2025-12-08 15:50:00'
# DATEDIFF 计算两个日期相差的天数
SELECT DATEDIFF('2025-12-10', '2025-12-08'); # 2
```

### 4、聚合函数

```sql
# COUNT 统计数量
SELECT COUNT(*) FROM users;
# SUM 求和
SELECT SUM(salary) FROM employees;
# AVG 求平均值
SELECT AVG(score) FROM students;
# MAX MIN 获取最大最小值
SELECT MAX(price), MIN(price) FROM products;
```

### 5、流程控制函数

```sql
# IF 条件判断
SELECT IF(1 > 0, 'Yes', 'No'); # 'Yes'
# CASE 多条件判断
SELECT 
  name,
  CASE 
    WHEN score >= 90 THEN 'A'
    WHEN score >= 80 THEN 'B'
    ELSE 'C'
  END AS grade
FROM students;
```

## 五、MySQL 的约束

我们在建表时可以给每个字段加上约束，约束是作用在字段上的规则，通过它可以保证数据库中数据的正确性、有效性和完整性。

MySQL 中主要提供了以下几种约束：

| 约束       | 关键字         | 作用                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| 主键约束   | PRIMARY KEY    | 确保该字段是行记录的唯一标识，一个表只能有一个主键约束       |
| 自增约束   | AUTO_INCREMENT | 确保该字段是自增且唯一的，一个表只能有一个自增约束并且只能用于整数列 |
| 唯一约束   | UNIQUE         | 确保该字段是唯一的，不会重复的                               |
| 非空约束   | NOT NULL       | 确保该字段是不为空的                                         |
| 检查约束   | CHECK          | 确保该字段满足自定义的规则                                   |
| 外键约束   | FOREIGN KEY    | 确保该字段引用的是另一张表中存在的值                         |
| 默认值约束 | DEFAULT        | 确保该字段如果不指定值的话，会有一个默认值                   |
