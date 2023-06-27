# 数据库笔记

>数据库==database
>
>数据库管理系统==DBMS（database management system）
>
>关系数据库==RDB（relational database）

[toc]

# 1.数据库基本信息




## 一、数据库种类

​	数据库以**数据保管形式**区分，有五种。

### 层次数据库 HDB

### 关系数据库 RDB

### 面向对象数据库 OODB

​	配合面向对象的编程语言，用来保管**对象**的数据库。

### XML数据库

### 键值存储系统



## 二、数据库结构

- 关系数据库以**行**为单位读写数据



## 三、SQL摘要

>SQl是操作**关系数据库**的**语言**，是一门语言
>
>一般以分号结尾
>
>不同的RDBMS有不用的sql标准
>
>sql根据目的分为DDL，DML，DCL

### SQL语句及种类

- DDL		创建删除

```mysql
create:创建数据库和表等对象
drop：删除数据库和表等对象
alter：修改数据库和表等对象的结构
```

- DML		查询更改

```mysql
select:查询数据
insert:插入新数据
update:更新数据
delete:删除数据
```

- DCL		确认取消变更，设定权限

```mysql
commit:确认对数据库中的数据进行变更
rollback：取消变更
grant：赋予权限
revoke：取消权限
```



### SQL书写规则

- **分号`;`结尾**

- **关键词不区别大小写**

- **常数的书写**

  - sql语句含有**字符串**

    书写规则是` 'abc'`，使用**单引号**括起来，表示字符串

  - 含有**日期**

    使用**单引号**括起来，日期的格式有很多种，像`26 JUN 2010`或者`10/01/26`等，一般统一使用`2010-01-26`这种**`年-月-日`**的格式。

- **数字无格式**



## 四、表的创建

### 创建数据库

```mysql
create database <xxx>;
create database shop;
```

### 表的创建

```mysql
create table <xxx>
(<列1名称> <数据类型> <该列所需约束>,
 <列2名称> <数据类型> <所需约束>，
	...      ...       ...     
 
 <该表的约束1>，<该表的约束2>，......);
```

```mysql
create table product
(product_id		 			CHAR(4)		      not null,
 product_name  			VARCHAR(100)    not null,
 product_type  			VARCHAR(32)     not null,
 sale_price    			INTEGER         ,
 purchase_price			INTEGER			  	,
 regist_date				DATE						,
 primary key (product_id));
```

⚠️:如果复制粘贴进shell，记得注意**字段名称**和**字段类型**是否粘在一起。

```
例子：
在文本栏： purchase_price INTEGER,
shell ：  pruchase_priceINTEGER,
```

如果粘在一起就会报错，所以最好一行一行复制进去，观察是否出现复制错误。

### 命名规则

- 只能使用**半角英文字母**、**数字**、**下划线**作为数据库、表的名称。
- 名称以**半角英文字母开头**。
- 名称不能重复。

### 数据类型

- integer：整数类型（不能存储小数）
- char：需要指定最大长度，类似`char(20)`这样，是**定长字符串**。如果字符串未达到最大长度，会用空格补全。

- varchar：存储字符串，需要指定长度`varchar(20)`，但是是**可变长字符串**，不会用空格补全。
- date：

### 约束设置

指的是对**列**中数据，限制和追加条件。

```mysql
product_id		char(4)		not null,
```

`not null`：`null`是空白，加上`not`表示该列的设置为不能输入空白。

```mysql
primary key (product_id)
```

这是给`product_id`设置**主键约束**，指特定一行数据，唯一确定一行数据。



## 五、表的删除和更新

### 表的删除

```mysql
drop table <xxx>;
```

⚠️:删除的表**无法恢复**，使用`drop`请务必注意。

### 表定义的更新

- 添加列的语法
- alter 就是变更

```mysql
alter table <表名> add column <列的定义>;
alter table product add column product_name_pinyin varchar(100);
```

- 删除表中某列

```mysql
alter table <表名> drop column <列名>;
alter table product drop column product_name_pinyin;
```

⚠️:变更之后无法恢复。

### 向表中插入数据

- 在mysql中使用`start transaction;`来进行插入。
- 用`commit;`来结束。

```mysql
start transaction;

insert into product values ('0001','Tshirt','衣服',1000,500, '2009-09-20');
insert into product values ('0002','打孔器','办公文具',500, 320,'2009-09-11');
  					......					......							....
  					
insert into <表名>  values (   <各种格式的数据>  );

commit;
```

不同的表，开始插入的写法都不一样，结尾都需要`commit`。

### 表名的修改

各种数据库修改表名的写法不一样，本文展示mysql的写法。

```mysql
rename table <修改前> to <修改后>;
```

# 2.查询语法

## 一、SELECT语句

### 列的查询

- select

```mysql
select <列名1>,....<列名n>
from <表名>；
```

- 修改列的名称
- as

```mysql
select <列名1> as <自己构思的别名> ,
			 <列名2> as <别称2>
from <表名>;
```

```mysql
select product_id as id,
		   product_name as xxx2
from product;

$ 或者使用中文别名,中文需要`""`括起来.
select xxx as "中文别名"
from xxx;
```

输出:

| id |xxx2|
| --- |---|
| xxx1 |xxx2|

### 查询表中所有的列

```mysql
select *
from <表名>;
```

使用`*`无法自定义显示的列的顺序

### 常数的查询





