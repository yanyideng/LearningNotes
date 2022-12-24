# 数据处理函数

## 常用文本处理函数

函数 | 说明
:--: | :--:
Left() | 返回串左边的字符
Length() | 返回串的长度
Locate() | 找出串的一个子串
Lower() | 将串转为小写
LTrim() | 去掉串左边的空格
Right() | 返回串右边的字符
RTrim() | 去掉串右边的空格
Soundex() | 返回串的SOUNDEX值。SOUNDEX是将任何文本串转为描述其语音表示的字母数字模式的算法。
Substring() | 返回子串的字符
Upper() | 将串转为大写

## 常用日期和时间处理函数

函数 | 说明
:--: | :--:
AddDate() | 增加一个日期（天、周等）
AddTime() | 增加一个时间（时、分等）
CurDate() | 返回当前日期
CurTime() | 返回当前时间
Date() | 返回日期时间的日期部分
DateDiff() | 计算两个日期之差
Date_Add() | 高度灵活的日期运算函数
Date_Format() | 返回一个格式化的日期或者时间串
Day() | 返回一个日期的天数部分
DayOfWeek() | 对于一个日期，返回对应的星期几
Hour() | 返回一个时间的小时部分
Minute() | 返回一个时间的分钟部分
Month() | 返回一个日期的月份部分
Now() | 返回当前日期和时间
Second() | 返回一个时间的秒部分
Time() | 返回一个日期时间的时间部分
Year() | 返回一个日期的年份部分

使用例子：
```SQL
WHERE Date(order_date) BETWEEN '2015-09-01' AND '2015-09-30';
```

## 数值处理函数

函数 | 说明
:--: | :--:
Abs() | 返回一个数的绝对值
Cos() | 返回一个角度的余弦
Exp() | 返回一个数的指数值
Mod() | 返回除操作的余数
Pi() | 返回圆周率
Rand() | 返回一个随机数
Sin() | 返回一个角度的正弦
Sqrt() | 返回一个数的平方根
Tan() | 返回一个角度的正切

## SQL聚集函数

函数 | 说明
:--: | :--:
AVG() | 返回某列的平均值
COUNT() | 返回某列的行数
MAX() | 返回某列的最大值
MIN() | 返回某列的最小值
SUM() | 返回某列值之和

### AVG()函数
`AVG()`用来确定特定数值列的平均值，**忽略列值为NULL的行**。
```SQL
SELECT AVG(prod_price) AS avg_price
```

### COUNT()函数
`COUNT()`用来计数。有两种用法：
1. 使用`COUNT(*)`对表中行的数目进行计数，不管表列中包含的是空值（NULL）还是非空值。
2. 使用`COUNT(column)`对特定列中具有值的行进行计数，**忽略NULL值**。

```SQL
SELECT COUNT(*) AS num_cust
FROM customers;
```

### MAX()函数
`MAX()`函数返回指定列中的最大值。用于文本数据时，如果数据按相应的列排序，则返回最后一行。**MAX()忽略列值为NULL的行**。

### MIN()函数
`MIN()`函数返回指定列中的最小值。用于文本数据时，如果数据按相应的列排序，则返回最前面的行。**MIN()忽略列值为NULL的行**。

### SUM()函数
`SUM()`用来返回指定列值的和。**忽略列值为NULL的行**。

### 聚集不同的值
上述五个聚集函数都可以如下使用：
1. 对所有行执行计算，指定`ALL`参数或者不给参数（ALL是默认行为）
2. 只包含不同的值，指定`DISTINCT`参数

`DISTINCT`必须使用列名，不能用于计算或者表达式，以及`COUNT(*)`。
```SQL
SELECT AVG(DISTINCT prod_price) AS avg_price
FROM products;
```
