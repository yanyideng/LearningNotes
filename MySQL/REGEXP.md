# 正则表达式

## 符号

符号  | 含义
:---: | :---:
.000 | '.' 匹配任意一个字符
1000 \| 2000 | '\|' 为OR操作符
[123] Ton | '[ ]' 匹配一组字符中的某个字符，此处为1、2、3中的其中一个字符
[^123] Ton | '[^...]' 为否定字符集，匹配不存在这些字符的表达式
[0-9] [a-z] | '[ ... - ... ]' 为范围匹配
\\\\. \\\\\\ | '\\\\' 为转义字符，MySQL要求两个反斜杠，自己解释一个，正则表达式库解释一个。'\\\\.'表示'.', '\\\\\\'表示'\\'
[:alnum:] | 字符类，预定义的字符集，详细见下一个表
\* | 0个或者多个匹配
\+ | 1个或者多个匹配
? | 0个或者1个匹配。例子为 'sticks?'，?匹配0个或1个s，即'stick'和'sticks'
{n} | n个匹配。例子为 '[[:digit:]]{4}'，匹配连续4个任意数字
{n,} | 不少于n个的匹配
{n,m} | n到m个匹配（m不超过255）
^word | 定位符^表示文本的开始。例子为 '^[0-9]'，匹配任意数字开头的字符串
word$ | 定位符$表示文本的结尾
[[:<:]] | 词的开始
[[:>:]] | 词的结尾

## 类

类   | 含义
:--: | :--:
[:alnum:] | 任意字母和数字
[:alpha:] | 任意字母
[:blank:] | 空格和制表符
[:cntrl:] | ASCII控制字符
[:digit:] | 任意数字
[:graph:] | 与[:print:]相同，但不包括空格
[:lower:] | 任意小写字母
[:print:] | 任意可打印字符
[:punct:] | 不在[:alnum:]和[:cntrl:]中的任意字符
[:space:] | 任意空白字符
[:upper:] | 任意大写字母
[:xdigit:] | 任意十六进制数字