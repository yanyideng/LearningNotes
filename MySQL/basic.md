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
WHERE prod_price <= 10 AND vend_id = 1003
ORDER BY prod_price DESC, prod_name --DESC只作用于它前面的列
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
LIMIT 3, 4;
--等同于
LIMIT 4   --取4行
OFFSET 3; --行3开始
```
WHERE子句可以用的操作符有：`=、!=、<、<=、>、>=、BETWEEN`。空值检查
```SQL
WHERE cust_email IS NULL;
```
WHERE子句可以用的逻辑操作符有：`AND、OR、IN、NOT`。使用圆括号分组逻辑操作符，保证优先级。
```SQL
WHERE vend_id IN (1002, 1003); --IN的用法
WHERE vend_id NOT IN (1002, 1003); --NOT否定后面的关键字
```

## 通配符和正则表达式
### 通配符
为了使用通配符，必须使用`LIKE`操作符。通配符有`'%'`和`'_'`两种。`'%'`表示任何字符出现任意次数(包括0次)。`'_'`只匹配单个字符(有且只有1次)。
```SQL
WHERE prod_name LIKE '%jet%';
WHERE prod_name LIKE '_ ton anvil';
```
***注意**，除非绝对有必要，否则不要把通配符用在模式的开始处，通配符放在开始处搜索起来最慢。

### 正则表达式
使用正则表达式必须用`REGEXP`操作符。
```SQL
WHERE prod_name REGEXP '1000'; --匹配包含文本'1000'的所有行
```

符号  | 含义
:---: | :---:
.000 | '.' 匹配任意一个字符
1000 \| 2000 | '\|' 为OR操作符
[123] Ton | '[ ]' 匹配一组字符中的某个字符，此处为1、2、3中的其中一个字符
[^123] Ton | '[^...]' 为否定字符集，匹配不存在这些字符的表达式



```SQL

```