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
SELECT prod_id, prod_name, SUM(prod_price) AS sum_price
FROM products
WHERE prod_price <= 10 AND vend_id = 1003
GROUP BY prod_id
HAVING COUNT(*) >= 2
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
使用正则表达式必须用`REGEXP`操作符。`LIKE`匹配整个字符串而`REGEXP`匹配子串。
```SQL
WHERE prod_name REGEXP '1000'; --匹配包含文本'1000'的所有行
```
详细的正则表达式符号和类在`REGEXP.md`中。

## 计算字段

### 拼接字段
`Concat()`函数用于拼接字段。`Trim() LTrim() RTrim()`用于去除空格。`AS`关键字赋予计算字段一个别名。
```SQL
SELECT Concat(RTrim(vend_name), ' (', RTrim(vend_country), ')') AS vend_title
FROM vendors
ORDER BY vend_name;
```

### 执行算术计算
MySQL中可以用`+ - * /`来对字段执行算术计算。
```SQL
SELECT quantity*item_price AS expanded_price
```

### 数据处理函数
详情见`functions.md`。
```SQL
SELECT Upper(vend_name) AS vend_name_upcase
```

## 分组数据 
分组允许把数据分为多个逻辑组，以便能对每个组进行聚集计算。使用SELECT语句的`GROUP BY`子句创建分组。例子：
```SQL
SELECT vend_id, COUNT(*) AS num_prods
FROM products
GROUP BY vend_id;
```
`GROUP BY`子句指示MySQL按vend_id排序并分组数据，所以对每个vend_id而不是整个表计算num_prods。即`GROUP BY`子句指示MySQL分组数据，然后对每个组而不是整个结果集进行聚集。
`GROUP BY`子句有一些重要的规定：
1. `GROUP BY`子句可以包含任意数目的列，这使得能对分组进行嵌套。
2. 如果进行了嵌套，数据将在最后的分组上进行汇总。
3. `GROUP BY`子句中列出的每个列都必须是检索列或者有效的表达式（但不能是聚集函数）。如果在SELECT中使用表达式，则必须在`GROUP BY`子句中指定相同的表达式。不能使用别名。
4. **除聚集计算语句外，SELECT语句中的每个列都必须在`GROUP BY`子句中给出**。
5. 如果分组列中具有NULL值，则NULL将作为一个分组返回。如果列中有多行NULL值，它们将分为一组。
6. `GROUP BY`子句必须出现在WHERE子句之后，ORDER BY子句之前。

MySQL允许过滤分组。使用`HAVING`子句过滤分组。例子：
```SQL
SELECT vend_id, COUNT(*) AS num_prods
FROM products
GROUP BY vend_id
HAVING COUNT(*) >= 3;
```
`HAVING`子句过滤了COUNT(*) >= 3（总数大于3的供应商）的那些分组。

`WHERE`子句过滤行，在数据分组前进行过滤；`HAVING`子句过滤分组，在数据分组后进行过滤，仅配合`GROUP BY`子句使用。




```SQL

```