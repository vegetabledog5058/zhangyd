# MYSQL综合查询练习(7/24)

## 数据:

<img src="https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/Typora202307241710400.png" style="zoom:40%;" />

### <font color='cornflowerblue'>1.周几赚的最多(dayofweek)</font>

!!!**注意：** 1=星期日，2=星期一，3=星期二，4=星期三，5=星期四，6=星期五，7=星期六。

DAYOFWEEK() 函数返回给定日期的工作日索引（从 1 到 7 的数字）。

DAYOFWEEK(*date*)

```sql
select dayofweek('2019-06-25');
+----------------------------------+
| dayofweek('2019-06-25 00:00:00') |
+----------------------------------+
|                                3 |
+----------------------------------+

select dayofweek(cast(20190625 as date));
+-----------------------------------+
| dayofweek(CAST(20190625 AS DATE)) |
+-----------------------------------+
|                                 3 |
+-----------------------------------+
```

------

CAST()函数，把一个字段转成另一个字段，主要转化的是字段的类型

其语法为：cast(字段名 as 转换的类型 )

```sql
            转换的类型共有：            CHAR            字符型

                                      DATE         日期型

                                      DATETIME  日期和时间型

                                      DECIMAL    float型

                                      SIGNED        int型

                                     TIME             时间型
```
------



```sql
数值:2015-11-03 15:31:26

select cast(date as signed) as date from  table1;
-- 结果：
20151103153126
 
select cast(date as char) as date from  table1;
-- 结果：
2015-11-03 15:31:26
 
select cast(date as datetime) as date from  table1;
-- 结果
2015-11-03 15:31:26
 
select cast(date as date) as date from  table1;
-- 结果
2015-11-03
 
select cast(date as time) as date from  table1;
-- 结果
15:31:26 
```



------



```sql
select dayofweek(cart.create_time) as 周几, max(cart.num*goods.price)
 as 总价
    ->  from cart,account,goods,category
    ->  where goods.good_no =cart.goods_no and account.id= cart.account_id and category.no = goods.category_no
    ->  group by cart.create_time;
```

![image-20230724212702876](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/Typora202307242127906.png)

### <font color='red'>2.购物车哪个货物利润最高(group by 与聚合函数用法)</font>

```sql
select goods.good_name,(sum((price-cost)*num))/cost as 利润率
    -> from account,cart,goods,category
    -> where goods.good_no = cart.goods_no
    -> and category.no = goods.category_no
    -> and account.id = cart.account_id
    -> group by goods.good_name,cost;
```

![image-20230724214226467](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/Typora202307242142505.png)

### 3.每个用户购物车总额()

```sql
select account.name, sum(num*price) as 总额
    -> from account,cart,goods,category
    -> where goods.good_no = cart.goods_no
    -> and category.no = goods.category_no
    -> and account.id = cart.account_id
    -> group by account.name;
```

![image-20230724213329499](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/Typora202307242133548.png)

### <font color='orange'>4.求2023年3月12日前一周销售的商品(date_add与date_sum)</font>



```sql
DATE_ADD(date,INTERVAL expr type)
DATE_SUM(date,INTERVAL expr type)

```

```SQL
SELECT OrderId,DATE_ADD(OrderDate,INTERVAL 2 DAY) AS OrderPayDate
FROM Orders
```



------



```sql
select goods.good_name from cart,goods
    -> where cart.goods_no = goods.good_no
    -> and cart.create_time between date_sub('2023-03-12',interval 1 week) and '2023-03-12';
```

![image-20230724210943253](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/Typora202307242109283.png)

### 5.张三的购物时间在什么时候

```sql
select create_time
    -> from account,cart,goods,category
    -> where goods.good_no = cart.goods_no
    -> and category.no = goods.category_no
    -> and account.id = cart.account_id
    -> and account.name = '张三' and cart.num > 0;
```



### 6一周内哪一天的商品总价最高

在 `SELECT` 子句中，你只能选择被 `GROUP BY` 子句列出的列或使用聚合函数进行计算的列

### <font color='red'>7.每个商品剩余(group by 与聚合函数)</font>

```sql
select goods.good_name,count - sum(num) as 库
存
    -> from account,cart,goods,category
    -> where goods.good_no = cart.goods_no
    -> and category.no = goods.category_no
    -> and account.id = cart.account_id
    -> group by goods.good_name,goods.count;
```

![image-20230724205101692](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/Typora202307242051741.png)

### <font color='red'>8.求用户购买完东西后还有多少余额(group by 与聚合函数)</font>

```sql
select goods.good_name,count - sum(num) as 库存
    -> from account,cart,goods,category
    -> where goods.good_no = cart.goods_no
    -> and category.no = goods.category_no
    -> and account.id = cart.account_id
    -> group by goods.good_name;
```

![image-20230724205230079](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/Typora202307242052125.png)