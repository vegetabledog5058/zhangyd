# MYSQL约束

## 1.主键约束(PK)

主键约束最显著的特征是主键列中的值是不允许重复(唯一)的，通过主键约束可强制表 的实体完整性。当创建或更改表时可通过定义 primary key约束来创建主键。

- 一个表只 能有一个primary key约束
- primary key约束中的列不能接受NULL值。
- 不同表之间主键相关联

查看约束/查看表结构

```sql
SHOW CREATE TABLE table_name

DESC table_name;
```

![image-20230727130838631](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307271308715.png)



### 已有表中添加主键

```sql
alter table tab_name add constraint pk_name primary key (deptno);
```

![image-20230727131302935](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307271313968.png)



```sql
- 创建表时
CREATE TABLE `table_name` (
`id` int NOT NULL PRIMARY KEY,-- 设置主键
`name` varchar(20) ,
);
//NOT NULL 可省略
CREATE TABLE `table_name` (
`id` int NOT NULL,
`name` varchar(20) ,
PRIMARY KEY (`id`) -- 设置主键
);//
字段名后添加primary key
CREATE TABLE `table_name` (
`id` int NOT NULL,
`name` varchar(20) ,
constraint pk primary key(id) -- 设置主键
);//"constraint pk"可省略表示定义主键名

-- 设置主键是deptno
ALTER TABLE emp MODIFY empno INT PRIMARY KEY; -- 修改列的属性来添加主键约束
ALTER TABLE 表名称 ADD PRIMARY KEY(id);
ALTER TABLE dept ADD CONSTRAINT pk_name PRIMARY KEY(deptno);
1
```

![image-20230727133019259](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307271330324.png)

## 自增长列（标识列）

自增长列是 int 类型的，其值是 int 类型的，其值是由数据库自动维护的，是永远都不会 重复的，因此自增长是最适合作为主键列的。在创建表时，通过 auto_increment 关键字 来标识自增长列;

自增长列可以是主键列，也可以是唯一列（有唯一约 束的列）

特点：

-   标识列必须和一个Key搭配（Key指主键、唯一、外键....）

- 一个表最多有一个标识列 

- 标识列的类型只能是数值型 

- 标识列可以通过SET auto_increment_increment = 3;设置步长（全局），也可以通过插入 行时手动插入标识列值设置起始值。

   

  ```sql
  SET @@auto_increment_increment = 3;(步长为3)
  SET auto_increment_increment = 3;
  
  
  CREATE TABLE table_name (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    age INT
  ) AUTO_INCREMENT=200; -- 设置自增长列的起始值为200
  
  
  ALTER TABLE tb_1 AUTO_INCREMENT=10;//修改步长起始值
  
  ```

  ![image-20230727160858194](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307271608295.png)

思考：什么情况下此设置会失效

在 MySQL 中，全局的自增长步长值是在会话级别进行设置的。当您更换用户或者关闭数据库连接后，会话会结束，全局的自增长步长值设置将会失效。

## 唯一约束(UQ)

对于非主键列中的值也要求唯一性时，就需要唯一约束

- 唯一约束要求值不能重复
-  可以存在多个空值( NULL )的数据 
- 一张表可以有多个唯一约束列

- 约束默认的名称为其列名 
- 唯一约束创建后会自动创建一个唯一索引(用show create table 可以查看)

```sql
-- 创建表时
CREATE TABLE `table_name` (
`id` int NOT NULL,
`name` varchar(20) unique, # 唯一约束  //
    
--已有表中添加新约束
ALTER TABLE 表名 ADD UNIQUE (列名);
    
--删除约束
ALTER TABLE your_table_name
DROP INDEX index_name;
    
INDEX INDEX unique_name on table_name;
```

![image-20230727193141507](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307271931541.png)

![image-20230727212212126](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307272122163.png)

## 默认约束(DF)与非空约束(NOT NULL)

默认约束:为列中的值设置默认值，default ....,如果已经定了值，默认值就无效了

NOT NULL ：非空，用于保证该字段的值不能为空。例如学生表的学生姓名及学号等等



为列中的值设置默认值，default ....,如果已经定了值，默认值就无效了默认为0

```sql
//创建表时设置默认值
CREATE TABLE `table_name` ( 
    `id` int DEFAULT (NOT) NULL,# 默认约束 
    `name` varchar(20) unique, 
);


//为已存在的表设置默认约束或非空约束, modify set,alter均可
ALTER TABLE table_name
CHANGE COLUMN column_name column_name data_type [DEFAULT new_default_value];

ALTER TABLE table_name
ALTER COLUMN column_name SET DEFAULT new_default_value;

ALTER TABLE table_name
ALTER wh SET DEFAULT new_default_value;

//如 ALTER TABLE tb_df
  ALTER wh SET DEFAULT 'xian';

```

- 创建表时，不写默认值都默认 NULL （在无非空约束的情况下）
- 默认约束能和主键约束可以同时存在
- 默认约束不能和 AUTO_INCREMENT 同时使用(用时刻函数时不冲突)

### 例:

下面是一个UQ与DF与非空的表

```sql
//建立表格
create table tb_df
(
id int,
name varchar(20),
wh varchar(10) default "beijin", //默认约束
undf varchar(10) unique not null,//非空约束
dfun int unique default 2   //唯一约束与默认约束

);
```

![image-20230727201414731](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307272014784.png)

### 插入数据

![image-20230727202415155](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307272024206.png)

注:默认值的修改只会对未来添加的新值作用,以及存在的值只能通过修改或者删除改变.

![image-20230727205252159](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307272052192.png)

并且使用 `UPDATE` 语句删除某一行中某一列的值，不会显示默认值，因为删除操作并不会修改表结构或列定义。它只是将指定列的值设置为 `NULL` 或其他默认值，而不会改变列的属性。

![image-20230727205849503](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307272058544.png)





### 删除约束

```sql
//去除默认值(null)
alter table 表名称 modify column 列名 列类型; -- 将默认值改为 NULL
//去除默认值的存在
ALTER TABLE tb_name ALTER col_name DROP DEFAULT; -- 删除了默认值，新增时必须有值
```

![image-20230727210753539](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307272107624.png)



## 外键约束

A表中列的值来自于另外一张表B的主键或唯一键的列称为 外键FK，将被引用值得表称为 主表或父表，将引用值得表称为从表或子表。 例如: emp 表中有 deptno 列，值来自于 de pt 表的 主键 deptno 。 dept 是主表， emp 是从表。

简单来说就是从表中是外键,主表中是主键,外键依赖于主键,与主键相同并且随主键改变而改变

```sql
-- 创建表时
CREATE TABLE `dept`(
dept_no INT PRIMARY KEY,
dept_name VARCHAR(20),
)


CREATE TABLE `emp` (
`id` int NOT NULL,
`name` varchar(20),
`deptno` int,
CONSTRAINT fk_dept_no FOREIGN KEY(deptno) REFERENCES dept(dept_no)
);


alter table userinfo add constraint foreign key fk_dept_no (dept_no) REFERENCES
dept(deptno);
-- 删除
ALTER TABLE tb_name DROP CONSTRAINT constraint_name;
alter table 表名称 drop foreign key 设置外键时的名称
```



- dept 是主表， userinfo 是从表 
- 在 userinfo 表中添加或修改时， dept_no 列的值必须是 dept 表中 deptno 字段中的 存在值或者 NULL 
- 删除从表数据可以直接删除 
- 删除主表数据时，会先检查被删除数据在从表中有没有对此数据的关联（引用），如果 有不能直接删除。



如果想要解除此限制需要先禁用外键约束【不推荐】 我们可以在创建约束时，设置级联操作【具体如何操作？】 



- on delete CASCADE/ on update CASCADE 级联删除 / 级联更新 
- ON DELETE SET NULL / ON UPDATE SET NULL

### 例题

![image-20230727235943501](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307272359540.png)

![image-20230728000002617](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307280000668.png)

#### 问题1:

employee表的 dept_id 列引用dept表的 dept_id 列

```sql
alter table employee add constraint foreign key dept_fpk (dept_id) references dept(dept_id);
```

用show create table查看表结构:

![image-20230728000303715](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307280003767.png)

#### 问题2:

删除测试部门及其员工

因为完整性原因需要先解除外键后进行级联删除故:

```sql
-- 先解除外键
 alter table employee drop FOREIGN KEY employee_ibfk_1;
 -- 然后将dept和employee表进行级联删除
 ALTER TABLE employee ADD constraint 
 FOREIGN KEY employee(dept_id) REFERENCES dept(dept_id) on delete CASCADE;
 -- 删除
 DELETE FROM dept WHERE dept_id=2;
```

![image-20230728000919797](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307280009853.png)