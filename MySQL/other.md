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

## 插入数据
一种插入数据方法：
```SQL
INSERT INTO customers
VALUES(NULL, 'Pep', '100', 'LA', 'CA', '90046','USA',NULL,NULL);
```
其中第一个值cust_id为NULL，是为了让MySQL完成自动增量的工作，最后两个NULL表示没有值。这种方法高度依赖表中列的定义次序，不安全。更安全的做法如下：
```SQL
INSERT INTO customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contract,cust_email)
VALUES('Pep', '100', 'LA', 'CA', '90046','USA',NULL,NULL);
```
这种方法在表后指定了列名。优点是即使表的结构改变了，此INSERT语句仍然能正常工作。其次使用这种语法可以省略列：cust_id的NULL值不是必要的，cust_id列也没有出现在列表中，所以不需要任何值。

需要同时插入多条数据时：
```SQL
INSERT INTO customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contract,cust_email)
VALUES('Pep', '100', 'LA', 'CA', '90046','USA',NULL,NULL),(xxxxxx);
```

### 插入检索出的数据
```SQL
INSERT INTO customers(cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contract,cust_email)
SELECT cust_name,cust_address,cust_city,cust_state,cust_zip,cust_country,cust_contract,cust_email
FROM customers;
```

## 更新数据
注意，不要省略WHERE子句，不然将更新所有行的数据。
```SQL
UPDATE customers
SET cust_name = 'The Fudds',
    cust_email = 'elmer@fudd.com'
WHERE cust_id = 10005;
```
如果用UPDATE语句更新多行，并且在更新某一行时出现了一个错误，则整个UPDATE操作被取消（以变更的值也将被恢复为原值）。如果使用了`IGNORE`关键字则发生了错误也继续更新：
```SQL
UPDATE IGNORE customers...
```
为了删除某个列，可以设置它为NULL（假如表定义允许NULL值）：
```SQL
UPDATE customers
SET cust_email = NULL
WHERE cust_id = 10005;
```

## 删除数据
注意，不要省略WHERE子句，不然将删除所有行的数据。
```SQL
DELETE FROM customers
WHERE cust_id = 10006；
```
1. `DELETE`将删除整个行而不是列，如果要删除指定的列，用`UPDATE`语句。
2. 即使`DELETE`删除所有行，也不会删除表本身。
3. 如果想从表中删除所有行，不要使用`DELETE`。可以使用`TRUNCATE TABLE`语句，它完成相同的工作，但速度更快（`TRUNCATE`实际上是删除原来的表并重新创建一个表，而不是一个个删除行的数据）。

## 操纵表
### 创建表
```SQL
CREATE TABLE customers
(
    cust_id         int         NOT NULL AUTO_INCREMENT,
    cust_name       char(50)    NOT NULL,
    cust_address    char(50)    NULL,
    quantity        int         NOT NULL DEFAULT 1,
    PRIMARY KEY(cust_id)
) ENGINE=InnoDB;
```
1. 创建新表时要注意指定的表名必须不存在，否则将出错。
2. NOT NULL指定列不接受没有值的行，NULL则接受（NULL为默认设置，不指定NOT NULL就默认NULL）。
3. 主键用`PRIMARY KEY(xxx, yyy, zzz)`指定。
4. `AUTO_INCREMENT`告诉MySQL本列增加一行时自动增量。每个表只允许一个`AUTO_INCREMENT`列，而且它必须被索引（如，使它成为主键）。
5. 可以通过`INSERT`语句插入一个有效值来覆盖`AUTO_INCREMENT`，后续的增量将从这个有效值开始。
   
### 更新表
```SQL
ALTER TABLE vendors
ADD vend_phone CHAR(20);

ALTER TABLE vendors
DROP COLUMN vend_phone;

--增加外键
ALTER TABLE orderitems
ADD CONSTRAINT fk_orderitems_orders
FOREIGN KEY (order_num) REFERENCES orders (order_num);
```

### 删除表
```SQL
DROP TABLE customers2;
```

### 重命名表
```SQL
RENAME TABLE customers2 TO customers;
```



```SQL

```