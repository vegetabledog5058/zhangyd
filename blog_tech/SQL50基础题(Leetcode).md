# SQL50基础题(Leetcode)

## 一.知识点引用

### 1.length与char_length()

- ​    length:返回字符串所占的字节数，是计算字段的长度一个汉字是算三个字符,一个数字或字母算一个字符
- ​    char_length:返回字符串所占的字符数，不管汉字还是数字或者是字母都算是一个字符

> 数字和字符相同()UTF8

<img src="https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308030039865.png" alt="c" style="zoom:40%;" />

> 当为英文字符以外时候也会有不同结果
>
> <img src="https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308030043222.png" style="zoom:50%;" />

对于SQL表，用于计算字符串中字符数的最佳函数是 [CHAR_LENGTH(str)](https://leetcode.cn/link/?target=https%3A%2F%2Fdev.mysql.com%2Fdoc%2Frefman%2F5.7%2Fen%2Fstring-functions.html%23function_char-length)，它返回字符串 `str` 的长度。

另一个常用的函数 LENGTH(str) 在这个问题中也适用，因为列 content 只包含英文字符，没有特殊字符。否则，LENGTH() 可能会返回不同的结果，因为该函数返回字符串 str 的字节数，某些字符包含多于 1 个字节。

### 2.关于NULL值的查询

首先观察下列表中,因为有空值,所以一定要注意;

MySQL 使用三值逻辑 —— TRUE, FALSE 和 UNKNOWN。所以任何与 NULL 值进行的比较都会与第三种值 UNKNOWN 做比较。这个“任何值”包括 NULL 本身！这就是为什么 MySQL 提供 IS NULL 和 IS NOT NULL 两种操作来对 NULL 特殊判断。

因此,想要进行查询,需要增加条件:referee_id IS NULL

```mysql
//第一种方法
SELECT name FROM customer WHERE referee_id != 2 OR referee_id IS NULL;
//第二种union all 解法

```

方法2,可以看见union all 与 union 的区别是 :

当使用union  时，mysql 会把结果集中重复的记录删掉，而使用union  all ，mysql 会把所有的记录返回，且效率高于union 

![image-20230803010511302](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308030105437.png)

![image-20230803005427609](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308030054831.png)

## 二.题目实例

1.

## 三.ii

