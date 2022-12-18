# MySQL

## 显示数据库和表信息
显示所有的数据库
```SQL
SHOW DATABASES;
```
选择数据库
```SQL
USE 数据库名; 
```
显示数据库中所有的表
```SQL
SHOW TABLES;
```
显示某个表中的所有字段信息
```SQL
SHOW COLUMNS FROM 表名;
DESCRIBE 表名; --MySQL支持
```

## SELECT语句
基本结构
```SQL
SELECT prod_id, prod_name
FROM products
LIMIT 5
OFFSET 3; --行数从0开始算，偏移3行（即行3开始）
```
检索所有列，会降低性能
```SQL
SELECT *
FROM products;
```
检索不同的行，DISTINCT关键字，作用于所有列而不仅是前置它的列
```SQL
SELECT DISTINCT vend_id, prod_price
FROM products;
```
限制结果数量。LIMIT加一个数字显示前n行；两个数字分别表示第几行开始，显示多少行（行数从0开始）。
```SQL
SELECT prod_name
FROM products
LIMIT 3, 4;
--等同于
LIMIT 4   --取4行
OFFSET 3; --行3开始
```

## 排序


```SQL

```