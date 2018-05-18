###SQL SELECT语句

```sql
select 列名称 from 表名称
select * from 表名称
```

| id   | name   | city    |
| ---- | ------ | ------- |
| 1    | white  | Beijing |
| 2    | john   | NewYork |
| 3    | Thomas | London  |

上述是一个"person"的表:

```sql
select * from person	#从上述表中选取所有数据
```

选取某一列或者某几列

```sql
select name from person
```

##select distinct 返回唯一不同的值

| company | num  |
| ------- | ---- |
| 完美    | 1235 |
| 京东    | 2456 |
| 完美    | 3789 |
| 小米    | 5897 |

```sql
select company from companys	#从表中选出所有公司包含重复值
```

```sql
select distinct company from companys	#仅选出不同公司
```

##where子句规定选择的标准

```sql
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
```

| 操作符  | 描述         |
| ------- | ------------ |
| =       | 等于         |
| <>/!=   | 不等于       |
| >       | 大于         |
| <       | 小于         |
| >=      | 大于等于     |
| <=      | 小于等于     |
| between | 在某个范围内 |
| like    | 搜索某种模式 |

**sql使用单引号环绕文本值(大部分系统也支持双引号)，如果是数值请不要使用引号**

##and & or用于基于一个以上的条件对记录进行过滤

*原始表*

| LastName | FirstName | Address        | City     |
| -------- | --------- | -------------- | -------- |
| Adams    | John      | Oxford Street  | London   |
| Bush     | George    | Fifth Avenue   | New York |
| Carter   | Thomas    | Changan Street | Beijing  |
| Carter   | William   | Xuanwumen 10   | Beijing  |

**and运算符实例**

```sql
SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'
```

**结果**

| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Carter   | Thomas    | Changan Street | Beijing |

**or运算符实例**

```sql
SELECT * FROM Persons WHERE firstname='Thomas' OR lastname='Carter'
```

**结果**



| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Carter   | Thomas    | Changan Street | Beijing |
| Carter   | William   | Xuanwumen 10   | Beijing |

**结合and和or**

```sql
SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='William')
AND LastName='Carter'
```

**结果**

| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Carter   | Thomas    | Changan Street | Beijing |
| Carter   | William   | Xuanwumen 10   | Beijing |

---

## ORDER BY语句用于对结果集进行排序

order by语句用于根据指定的列对结果集进行排序，默认是升序排列，如果希望降序排列可以使用DESC关键字

Orders 表:

| Company  | OrderNumber |
| -------- | ----------- |
| IBM      | 3532        |
| W3School | 2356        |
| Apple    | 4698        |
| W3School | 6953        |

```sql
#以字母顺序显示
select company,ordernumber from Orders order by company
#以数字顺序显示
select company,ordernumber from Orders order by ordernumber
#以逆字母序显示公司名称
select company,ordernumber from Orders order by company desc
#以数字逆序显示公司名称
select company,ordernumber from Orders order by ordernumber desc
```

---

## SQL INSERT INTO向表中插入新的行

```sql
insert into 表名 values (值1...值n)
#指定所要插入数据的列
insert into tablename (列1...列n) values (值1...值n)
```

### "Persons" 表：

| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Carter   | Thomas    | Changan Street | Beijing |

```sql
#插入一行
insert into Persons values('bill', 'Tom', 'BJStreet', 'BJ')
#插入指定列中元素
insert into Persons(LastName, Address) values('jim', 'TJStreet')
```

---

## update 用于修改表中的数据

```sql
update TableName set ColumnName = NewValue where ColumnName = 值
```

## Person:

| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Gates    | Bill      | Xuanwumen 10   | Beijing |
| Wilson   |           | Champs-Elysees |         |

```sql
#更新某一行中的某一列
update Person set FirstName = 'TOM' where LastName = 'Wilson'
#更新某一行若干列
update Person set FirstName = 'zh', LastName = 'J' where City = 'Beijing'
```

---

## DELETE删除表中的行

```sql
delete from TableName where ColumnName = 值
```

## Person:

| LastName | FirstName | Address      | City    |
| -------- | --------- | ------------ | ------- |
| Gates    | Bill      | Xuanwumen 10 | Beijing |
| Wilson   | Fred      | Zhongshan 23 | Nanjing |

```sql
#删除某一行
delete from Person where Lastname = 'Wilson'
#删除所有行 可以在不删除表的情况下删除所有行。
delete from TableName
#或者
delete * from TableName
```

---

# SQL 高级教程

## SQL TOP子句 用于规定要返回的记录数目

对于拥有数千条记录的大型数据表来说，TOP子句是非常有用的

**并非所有数据库都支持TOP**

---

```sql
#Sql Server
select TOP number | percent ColumnName(s) from TableName
#MySql
select ColumnName(s) from TableName LIMIT number
#e.g.
select * from Persons limit 5
#Oracle
select ColumnName from TableName where RowNum <= 5
#e.g.
select * from Persons where RowNum <=5
```



Persons 表:

| Id   | LastName | FirstName | Address             | City       |
| ---- | -------- | --------- | ------------------- | ---------- |
| 1    | Adams    | John      | Oxford Street       | London     |
| 2    | Bush     | George    | Fifth Avenue        | New York   |
| 3    | Carter   | Thomas    | Changan Street      | Beijing    |
| 4    | Obama    | Barack    | Pennsylvania Avenue | Washington |

```sql
#Sql
select top 2 * om Persons
select top 50 prcent * from Persons
```

---

## SQL LIKE操作符 用于在where子句中搜索列中的指定模式

```sql
select ColumnName（s） from TableName where ColumnName LIKE pattern
```

---

Persons 表:

| Id   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

```sql
#选择住在N开头的城市中
select * from Persons where City LIKE 'N%'
#选择住在以g结尾的城市中的人
select * from Persons where City LIKE '%g'
#选择居住地不在‘lon’中的人
select * from Persons where City NOT LIKE '%lon%'
```

---

## SQL 通配符 在搜索数据库时，SQL通配符可以替代一个或多个字符  通配符必须与LIKE一起使用 

在 SQL 中，可使用以下通配符：

| 通配符                     | 描述                       |
| -------------------------- | -------------------------- |
| %                          | 替代一个或多个字符         |
| _                          | 仅替代一个字符             |
| [charlist]                 | 字符列中的任何单一字符     |
| [^charlist]或者[!charlist] | 不在字符列中的任何单一字符 |

Persons 表:

| Id   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

## %通配符

```sql
#居住地以'Ne'开始城市的人
select * from Persons where City LIKE 'Ne%'
#选取居住地包含'lon'的人
select * from Persons where City LIKE '%lon%'
```

## _通配符

```sql
#选择第一个字符后是'eorge'的人
select * from persons where FirstName Like '_eorge'
#选择以'C'开头之后是任意字符然后是'er'的人
select * from persons where FirstName LIKE 'C_er'
```

##[charlist]通配符

```sql
#选取表中居住地以'A', 'S', 'N'开头的人
select * from Persons where FirstName LIKE '[ASN]%'
#选取表中居住地不以'A', 'S', 'N'开头的人
select * from Persons where FirstName Like '[!ASN]%'
select * from Persons where FirstName Like '[^ASN]%'
```

## IN操作符 规定我们在where子句中规定多个值

```sql
select ColumnName（s） from TableName where ColumnName IN (value1, value2....valuen)
```

---



Persons 表:

| Id   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street |          |

```sql
#从表中选取姓氏为Adams和Carter的人
select * from persons where LastName IN ('Adams', 'Carter')
```

---

## between操作符在where子句中使用，作用是选取介于两个值之间的数据范围 可以是文本，数值，日期

```sql
select ColumnName（s） from TableName where ColumnName between value1 and value2
```

---

Persons 表:

| Id   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |
| 4    | Gates    | Bill      | Xuanwumen 10   | Beijing  |

```sql
#显示介于'Adams'和‘Carter’(左闭右开)区间范围内的人
select * from persons where LastName between 'Adams' and 'Carter'
```

**不同数据库对between...and支持不同**

---

## SQL Alias别名 可以为列名和表名指定别名(alias)

```sql
#表的SQL Alias语法
select ColumnName from TableName AS AliasName
#列的SQL Alias语法
select ColumnName from AS AliasName from TableName
```

```sql
#假设我们有两个表分别是："Persons" 和 "Product_Orders"。我们分别为它们指定别名 "p" 和 "po"。
现在，我们希望列出 "John Adams" 的所有定单。
select po.OrderID, p.LastName,p.FirstName From Persons as p,
Product_Orderes as po where p.LastName = 'Adams' AND p.FirstName = 'John'

#不使用别名的select
select Product_Orders.OrderID, Persons.LastName, Persons.FirstName from Persons, Product_Oders where Persons.LastName = 'Adams' and Persons.FirstName = 'John'
```

### 表 Persons:

| Id   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

 ```sql
select LastName as Family, FirstName as Name from Persons
 ```

### 结果：

| Family | Name   |
| ------ | ------ |
| Adams  | John   |
| Bush   | George |
| Carter | Thomas |

---

## SQL JOIN用于根据两个或多个表中的列之间的关系，从这些表中查询数据

###Join和Key

有时为了得到完整的结果，我们需要从两个或更多的表中获取结果。我们就需要执行 join。

数据库中的表可通过键将彼此联系起来。主键（Primary Key）是一个列，在这个列中的每一行的值都是唯一的。在表中，每个主键的值都是唯一的。这样做的目的是在不重复每个表中的所有数据的情况下，把表间的数据交叉捆绑在一起。

请看 "Persons" 表：

| Id_P | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

请注意，"Id_P" 列是 Persons 表中的的主键。这意味着没有两行能够拥有相同的 Id_P。即使两个人的姓名完全相同，Id_P 也可以区分他们。

接下来请看 "Orders" 表：

| Id_O | OrderNo | Id_P |
| ---- | ------- | ---- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

请注意，"Id_O" 列是 Orders 表中的的主键，同时，"Orders" 表中的 "Id_P" 列用于引用 "Persons" 表中的人，而无需使用他们的确切姓名。

请留意，"Id_P" 列把上面的两个表联系了起来。

---

查找一个人所下的订单

```sql
select Persons.LastName, Persons.FirstName, Product_Orders.OrderNO from Persons, Orders where
Persons.Id_P = Orders.Id_P
```

结果集：

| LastName | FirstName | OrderNo |
| -------- | --------- | ------- |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

---

使用join的查找方法

```sql
select Persons.LastName, Persons.FirstName, Orders.OrderNO from Persons INNER join Orders ON Persons.Id_p = Orders.Id_p
Order by Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| -------- | --------- | ------- |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

---

## SQL Join的类型

Inner join 内连接

Join:如果表中至少有一个匹配，则返回行

LEFT Join：即使右表中没有匹配，也从左表中返回所有的行

RIGHT Join：即使左表中没有匹配，也从由表中返回所有的行

FULL Join：只要其中一个表存在匹配就返回行

## SQL INNER JOIN 关键字

在表中存在至少一个匹配时，INNER JOIN 关键字返回行。

### INNER JOIN 关键字语法

```
SELECT column_name(s)
FROM table_name1
INNER JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

注释：INNER JOIN 与 JOIN 是相同的。

## 原始的表 (用在例子中的)：

"Persons" 表：

| Id_P | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

"Orders" 表：

| Id_O | OrderNo | Id_P |
| ---- | ------- | ---- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

## 内连接（INNER JOIN）实例

现在，我们希望列出所有人的定购。

您可以使用下面的 SELECT 语句：

```
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| -------- | --------- | ------- |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

INNER JOIN 关键字在表中存在至少一个匹配时返回行。如果 "Persons" 中的行在 "Orders" 中没有匹配，就不会列出这些行。

## SQL left Join关键字 会从左表中返回所有的行，即使在右表中没有匹配的行

```sql
#语法
select ColumnName(s) from table1 left join table2 on
table1.colname = table2.colname
```

注释：某些数据库中，left join称为left outer join

---

## 左连接（LEFT JOIN）实例

现在，我们希望列出所有的人，以及他们的定购 - 如果有的话。

您可以使用下面的 SELECT 语句：

```sql
select Persons.LastName, Persons.FirstName, Orders.OrderNo
from Persons left join Orders on Persons.Id_p = Orders.Id_P ORDER BY Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| -------- | --------- | ------- |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
| Bush     | George    |         |

LEFT JOIN 关键字会从左表 (Persons) 那里返回所有的行，即使在右表 (Orders) 中没有匹配的行。

---

## SQL RIGHT JOIN 关键字

RIGHT JOIN 关键字会右表 (table_name2) 那里返回所有的行，即使在左表 (table_name1) 中没有匹配的行。

### RIGHT JOIN 关键字语法

```sql
select col(s) from table1 right join table2 on table1.col = table2.col
```

注释：在某些数据库中， RIGHT JOIN 称为 RIGHT OUTER JOIN。

---

## 原始的表 (用在例子中的)：

"Persons" 表：

| Id_P | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

"Orders" 表：

| Id_O | OrderNo | Id_P |
| ---- | ------- | ---- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

右连接(right john)实例

```sql
#希望列出所有的订单，以及订购的人-如果有的话
select Persons.LastName, Persons.FirstName, Orders.orderNo
from Persons right join Orders on Persons.Id_p = Orders.Id_p
order by Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| -------- | --------- | ------- |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
|          |           | 34764   |

RIGHT JOIN 关键字会从右表 (Orders) 那里返回所有的行，即使在左表 (Persons) 中没有匹配的行。

---

## SQL Full Join关键字 只要其中某个表存在匹配， Full join关键字就会返回行

```sql
#语法
select col(s) from table1 full join table2 on table1.col = table2.col
```

## 原始的表 (用在例子中的)：

"Persons" 表：

| Id_P | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

"Orders" 表：

| Id_O | OrderNo | Id_P |
| ---- | ------- | ---- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

```sql
#希望列出所有的人以及所有的订单
select Persons.LastName, Persons.FirstName, Orders.OrderNo full join Orders on Persons.Id_p = Orders.Id_p order by Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| -------- | --------- | ------- |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
| Bush     | George    |         |
|          |           | 34764   |

FULL JOIN 关键字会从左表 (Persons) 和右表 (Orders) 那里返回所有的行。如果 "Persons" 中的行在表 "Orders" 中没有匹配，或者如果 "Orders" 中的行在表 "Persons" 中没有匹配，这些行同样会列出。

---

## SQL Union 和Union All操作符

SQl Union操作符用于合并两个或者多个select语句的结果集

**注意**：Union内部的select语句必须拥有相同数量的列。列也必须拥有相似的数据类型，每条sql语句的列的顺序必须相同

```sql
#union语法
select col(s) from table1
union
select col(s) from table2
```

**注释**：默认，Union操作符选取不同的值，如果允许重复的值，请使用Union All

```sql
#union all
select col1(s) from table1
union all
select col2(s) from table2

```

Union结果集中的列名总等于Union中第一个select的列名



## 下面的例子中使用的原始表：

### Employees_China:

| E_ID | E_Name         |
| ---- | -------------- |
| 01   | Zhang, Hua     |
| 02   | Wang, Wei      |
| 03   | Carter, Thomas |
| 04   | Yang, Ming     |

### Employees_USA:

| E_ID | E_Name         |
| ---- | -------------- |
| 01   | Adams, John    |
| 02   | Bush, George   |
| 03   | Carter, Thomas |
| 04   | Gates, Bill    |

```sql
#列出中国和美国不同名的雇员
select E_NAME form Employees_China
union 
select E_NAME from Employees_USA
```

### 结果

| E_Name         |
| -------------- |
| Zhang, Hua     |
| Wang, Wei      |
| Carter, Thomas |
| Yang, Ming     |
| Adams, John    |
| Bush, George   |
| Gates, Bill    |

注释：这个命令无法列出在中国和美国的所有雇员。在上面的例子中，我们有两个名字相同的雇员，他们当中只有一个人被列出来了。UNION 命令只会选取不同的值。

Union All

```sql
#列出中国和美国的所有雇员
select E_NAME from Employees_China
union all 
select E_NAME from Employees_USA
```

### 结果

| E_Name         |
| -------------- |
| Zhang, Hua     |
| Wang, Wei      |
| Carter, Thomas |
| Yang, Ming     |
| Adams, John    |
| Bush, George   |
| Carter, Thomas |
| Gates, Bill    |

---

## Select into 用于创建表的备份复件

select into 语句从一个表中选取数据，然后把数据插入另一个表中

select into语句常用于创建表的备份复件或者用于对记录进行存档

```sql
#把所有列插入新表
select * into NewTable [IN extrnaldatabase] from old_table
#把需要的列插入新表
select col(s) into NewTable [IN extrnaldatabase] from old_table
```

---

```sql
#制作Persons表的备份
select * into PersonsBackup from Persons
#in 子句可以用于向数据库中拷贝表
select * into Persons IN 'BackUP.mdb' from Persons
#如果只需要拷贝某些域
select col(s) into PersonsBackup from Persons
```

---

```sql
#通过从'Persons'表中提取居住在'Beijing'的人的信息，创建一个带有两个列的名为"PersonsBackUP"的表
select LastName FirstName into PersonsBackup from Persons where City = 'Beijing'
```

从一个以上的表中选取数据也是可以做到的。

下面的例子会创建一个名为 "Persons_Order_Backup" 的新表，其中包含了从 Persons 和 Orders 两个表中取得的信息：

```sql
select Persons.LastName, Orders.OrderNo into PersonsOrderBackUP from Persons inner join Orders on Persons.Id_p = Orders.Id_p
```

---

## 创建数据库

```sql
create database DatabaseName
```

## 创建数据库表

```sql
create table TableName
(
    col1 dataType,
    col2 dataType,
    coln dataType,
    ...
)
```

数据类型（data_type）规定了列可容纳何种数据类型。下面的表格包含了SQL中最常用的数据类型：

| 数据类型                                          | 描述                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| integer(size)int(size)smallint(size)tinyint(size) | 仅容纳整数。在括号内规定数字的最大位数。                     |
| decimal(size,d)numeric(size,d)                    | 容纳带有小数的数字。"size" 规定数字的最大位数。"d" 规定小数点右侧的最大位数。 |
| char(size)                                        | 容纳固定长度的字符串（可容纳字母、数字以及特殊字符）。在括号中规定字符串的长度。 |
| varchar(size)                                     | 容纳可变长度的字符串（可容纳字母、数字以及特殊的字符）。在括号中规定字符串的最大长度。 |
| date(yyyymmdd)                                    | 容纳日期。                                                   |

---

## SQL 约束

## SQL 约束

约束用于限制加入表的数据的类型。

可以在创建表时规定约束（通过 CREATE TABLE 语句），或者在表创建之后也可以（通过 ALTER TABLE 语句）。

我们将主要探讨以下几种约束：

- NOT NULL
- UNIQUE
- PRIMARY KEY
- FOREIGN KEY
- CHECK
- DEFAULT

注释：在下面的章节，我们会详细讲解每一种约束。

---

SQL not null 约束

强制不接受NULL值

强制字段必须始终包含值，如果不向字段中添加值，就无法插入新记录或更新记录

```sql
create table Persons
(
    Id_P int not null,
    LastName varchar(255) not null,
    FirstName varchar(255),
    Address varchar(255)
)
```

---

SQL unique约束

unique约束唯一标识数据库中每条记录

unique和primary key约束均为列或列集合提供了唯一性保证

primary key拥有自定义的unique约束

每个表可以有多个unique约束，但是只能有一个主键

```sql
#SQL unique 约束在创建数据库表的使用
#Mysql
create table Persons
(
    Id_P int not null,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    unique(Id_P)
)
#Sql server Oracle MS Access
create table Persons  
(
    Id_P int not null unique,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
)
#多个约束
CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT uc_PersonID UNIQUE (Id_P,LastName)
)
```

## SQL UNIQUE Constraint on ALTER TABLE

当表已被创建时，如需在 "Id_P" 列创建 UNIQUE 约束，请使用下列 SQL：

```sql
#额外创建约束
alter table Persons add constraint uc_PersonID unique (Id_P, LastName)
#撤销约束
#Mysql
alter table Persons Drop INDER uc_PersonID
#其他
alter table Persons Drop constraint uc_PersonID
```

---

## SQL PRIMARY KEY约束

主键必须包含唯一值，主键列不能为空，每个表都应该有一个主键，并且每个表只能有一个主键

---

```mysql
#mysql
create database Persons
(
    Id_p int not null,
    LastName varchar(255) not null,
    FirstName varchar(255) not null,
    primary key(Id_p)
)
#sql server 
CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT pk_PersonID PRIMARY KEY (Id_P,LastName)
)
```

## SQL PRIMARY KEY Constraint on ALTER TABLE

如果在表已存在的情况下为 "Id_P" 列创建 PRIMARY KEY 约束，请使用下面的 SQL：

### MySQL / SQL Server / Oracle / MS Access:

```
ALTER TABLE Persons
ADD PRIMARY KEY (Id_P)
```

如果需要命名 PRIMARY KEY 约束，以及为多个列定义 PRIMARY KEY 约束，请使用下面的 SQL 语法：

### MySQL / SQL Server / Oracle / MS Access:

```
ALTER TABLE Persons
ADD CONSTRAINT pk_PersonID PRIMARY KEY (Id_P,LastName)
```

注释：如果您使用 ALTER TABLE 语句添加主键，必须把主键列声明为不包含 NULL 值（在表首次创建时）。

## 撤销 PRIMARY KEY 约束

如需撤销 PRIMARY KEY 约束，请使用下面的 SQL：

### MySQL:

```
ALTER TABLE Persons
DROP PRIMARY KEY
```

### SQL Server / Oracle / MS Access:

```
ALTER TABLE Persons
DROP CONSTRAINT pk_PersonID
```

---

SQL Foreign key约束

一个表中的Foreign key指向另一个表中的Primary key

让我们通过一个例子来解释外键。请看下面两个表：

"Persons" 表：

| Id_P | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

"Orders" 表：

| Id_O | OrderNo | Id_P |
| ---- | ------- | ---- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |

请注意，"Orders" 中的 "Id_P" 列指向 "Persons" 表中的 "Id_P" 列。

"Persons" 表中的 "Id_P" 列是 "Persons" 表中的 PRIMARY KEY。

"Orders" 表中的 "Id_P" 列是 "Orders" 表中的 FOREIGN KEY。

FOREIGN KEY 约束用于预防破坏表之间连接的动作。

FOREIGN KEY 约束也能防止非法数据插入外键列，因为它必须是它指向的那个表中的值之一。

## SQL FOREIGN KEY Constraint on CREATE TABLE

下面的 SQL 在 "Orders" 表创建时为 "Id_P" 列创建 FOREIGN KEY：

```mysql
#Mysql
create table Orders
(
    Id_O int not null,
    OrderNo int not null,
    Id_p int,
    Primary Key (Id_O),
    foreign key (Id_p) references Persons(Id_p)
)
```

```sql
#sql server/oracle/access
CREATE TABLE Orders
(
	Id_O int NOT NULL PRIMARY KEY,
	OrderNo int NOT NULL,
	Id_P int FOREIGN KEY REFERENCES Persons(Id_P)
)
```

如果需要命名 FOREIGN KEY 约束，以及为多个列定义 FOREIGN KEY 约束，请使用下面的 SQL 语法：

```mysql
 CREATE TABLE Orders
(
	Id_O int NOT NULL,
	OrderNo int NOT NULL,
	Id_P int,
	PRIMARY KEY (Id_O),
	CONSTRAINT fk_PerOrders FOREIGN KEY (Id_P)
	REFERENCES Persons(Id_P)
)

```

---

## SQL FOREIGN KEY Constraint on ALTER TABLE

如果在 "Orders" 表已存在的情况下为 "Id_P" 列创建 FOREIGN KEY 约束，请使用下面的 SQL：

```mysql
alter table Orders add foreign key (Id_P) references Persons(Id_P)
```

如果需要命名 FOREIGN KEY 约束，以及为多个列定义 FOREIGN KEY 约束，请使用下面的 SQL 语法：

### MySQL / SQL Server / Oracle / MS Access:

```mysql
alter table Orders add constraint fk_PerOrders foreign key (Id_P) references Persons(Id_P)
```

---

## 撤销 FOREIGN KEY 约束

如需撤销 FOREIGN KEY 约束，请使用下面的 SQL：

```mysql
#mysql
alter table Orders drop foreign key fk_PreOrders
#sql server 
alter table Orders drop constraint fk_PerOrders
```

---

## SQL Check约束

用于限制列中值得范围

对于单个列定义check约束，那么该列只允许特定的值

对于一个表定义约束check，那么此约束会在特定的列中对值进行限制

---

## SQL Check Constraint on create table

```mysql
#create table Persons并且设置Id_p字段约束大于0
#mysql
(
    Id_P int not null,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City carchar(255),
    check(Id_P > 0)
)
#其他
create table Persons
(
    Id_P int nut null check(id_p > 0)
    LastName varchar(255),]
    ...
)
```

```mysql
#需要命名check约束以及为多个列定义check约束
create table Persons
(
    Id_P int not null,
    LastName varchar(255) not null,
    FirstNamr varchar(255),
    Address varchar(255),
    City varchar(255),
    constraint chk_Person check (Id_P And City='Sandnes')
)
```

---

## SQL check constraint on alter table

```mysql
#在表已存在的情况下为Id_P列创建check约束
alter table Persons add check (Id_P > 0)
```

```mysql
#命名以及定义多个check约束
alter table Persons add constraint chk_person check(Id_P > 0 and city='Sandnes')
```

---

## 撤销check约束

```mysql
#sql server access oracle
alter table Persons drop constraint chk_Person
#mysql
alter table Persons drop check chk_Person
```

---

## SQL default约束

default约束用于向列中插入默认值

如果没有规定其他的值，那么会将默认值添加到所有的新纪录

---

## SQL Default constraint on create table

```mysql
create table Persons
(
    Id_P int not null,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) default 'Sandnes'
)
```

---

通过使用getdata()函数，default约束也可以用于插入系统值

```mysql
create table Orders
(
    Id_O int not null,
    OrderNo int not null,
    Id_P int,
    OrderDate date default getdate()
)
```

---

## SQL default constraint on alter table

```mysql
#表存在的情况下为字段创建default约束
#mysql
alter table Persons alter city set default 'sandy'
#sql server
alter table Persons alter column city set default 'sndy'
```

---

## SQL撤销约束

```mysql
#Mysql
alter table Persons alter city drop default
#sql server ....
alter table Persons alter column city drop default
```

---

## SQL index在不读取整个表的情况下，索引使数据库应用程序可以更快的查找数据

---

**索引**

可以通过在表中创建索引，仪表更快的查询数据

用户看不到索引，索引只是被用来加速搜索或查询

***注释***：更新一个包含索引表更加耗时，由于索引本身也许要更新。比较理智的做法是在常常被搜索的列(以及表)上创建索引

SQL index语法

```mysql
#在表上创建一个简单索引，允许使用重复的值
create index indexName on tableName(columnName)
```

SQl  create unique index

```mysql
create unique index indexName on tableName(columnName)
```

---

create index实例

```mysql
#在LastName列上创建一个升序的索引
create index PersonIndex on Person(LastName)
#降序
create index PersonIndex on Person(LastName desc)
#如果创建多个索引
create index PersonIndex on person(LastName, FirstName)
```

---

## SQL撤销索引，表以及数据库

通过drop语句，可以轻松删除索引，表以及数据库

SQL Drop index语句

可以使用drop index命令删除表格中的索引

```mysql
#sql lite access
drop index indexName on tableName
#sql server
drop index tableName.indexName
#IBM DB2和oracle
drop index indexName
#mysql
alter table tableName drop index indexName
```

---

## 删除数据库表（表的结构，属性以及索引都会被删除）

```mysql
drop table tableName
```

## 删除数据库

```mysql
drop database databaseName
```

---

Sql truncate table 语句仅仅删除表内数据，但是并不删除表本身

```mysql
truncate table tableName
```

---

## SQL alter table语句 用于在已有的表中添加，修改或删除列

SQL alter table语法

```mysql
#添加列
alter table tableName add columnName databyte
#删除列
alter table tableName drop column columnName 
```

***注释***：注释：某些数据库系统不允许这种在数据库表中删除列的方式 (DROP COLUMN column_name)。

做法如下：

```mysql
alter table tableName
alter column columnName databyte
```

---

## 原始的表 (用在例子中的)：

Persons 表:

| Id   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

SQL alter table

```mysql
#在person表中添加一个名为Birthday的新列
alter table Persons add Birthday date
```

| Id   | LastName | FirstName | Address        | City     | Birthday |
| ---- | -------- | --------- | -------------- | -------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |          |
| 2    | Bush     | George    | Fifth Avenue   | New York |          |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |          |

---

改变数据类型

```mysql
#改变Birthday数据类型
alter table Persons 
alter column Birthday year
```

请注意，"Birthday" 列的数据类型是 year，可以存放 2 位或 4 位格式的年份。

---

drop column

```mysql
#删除Persons中的Birthday实例
alter table Person drop column Birthday
```

| Id   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

---

## SQL Auto increment字段 会在新纪录插入表中时生成一个唯一数字

通常希望在每次插入新记录时，自动的常见主键字段的值

我们可以在表中创建一个auto-increment字段

---

```mysql
create table Persons
(
    P_id not null auto_increment,
    LastName varchar(255), not null
    ...
)
```

MySQL 使用 AUTO_INCREMENT 关键字来执行 auto-increment 任务。

默认地，AUTO_INCREMENT 的开始值是 1，每条新记录递增 1。

```mysql
#以其他值作为起始值
alter table Persons auto_increment = 100
```

```mysql
#在Persons表中插入记录，不必为P_id列规定值
insert into Persons(FirstName, LastName) values('Bill', 'Gates')
```

---

## 用于 SQL Server 的语法

下列 SQL 语句把 "Persons" 表中的 "P_Id" 列定义为 auto-increment 主键：

```
CREATE TABLE Persons
(
P_Id int PRIMARY KEY IDENTITY,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)
```

MS SQL 使用 IDENTITY 关键字来执行 auto-increment 任务。

默认地，IDENTITY 的开始值是 1，每条新记录递增 1。

要规定 "P_Id" 列以 20 起始且递增 10，请把 identity 改为 IDENTITY(20,10)

要在 "Persons" 表中插入新记录，我们不必为 "P_Id" 列规定值（会自动添加一个唯一的值）：

```
INSERT INTO Persons (FirstName,LastName)
VALUES ('Bill','Gates')
```

上面的 SQL 语句会在 "Persons" 表中插入一条新记录。"P_Id" 会被赋予一个唯一的值。"FirstName" 会被设置为 "Bill"，"LastName" 列会被设置为 "Gates"。

## 用于 Access 的语法

下列 SQL 语句把 "Persons" 表中的 "P_Id" 列定义为 auto-increment 主键：

```
CREATE TABLE Persons
(
P_Id int PRIMARY KEY AUTOINCREMENT,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)
```

MS Access 使用 AUTOINCREMENT 关键字来执行 auto-increment 任务。

默认地，AUTOINCREMENT 的开始值是 1，每条新记录递增 1。

要规定 "P_Id" 列以 20 起始且递增 10，请把 autoincrement 改为 AUTOINCREMENT(20,10)

要在 "Persons" 表中插入新记录，我们不必为 "P_Id" 列规定值（会自动添加一个唯一的值）：

```
INSERT INTO Persons (FirstName,LastName)
VALUES ('Bill','Gates')
```

上面的 SQL 语句会在 "Persons" 表中插入一条新记录。"P_Id" 会被赋予一个唯一的值。"FirstName" 会被设置为 "Bill"，"LastName" 列会被设置为 "Gates"。

## 用于 Oracle 的语法

在 Oracle 中，代码稍微复杂一点。

您必须通过 sequence 对创建 auto-increment 字段（该对象生成数字序列）。

请使用下面的 CREATE SEQUENCE 语法：

```
CREATE SEQUENCE seq_person
MINVALUE 1
START WITH 1
INCREMENT BY 1
CACHE 10
```

上面的代码创建名为 seq_person 的序列对象，它以 1 起始且以 1 递增。该对象缓存 10 个值以提高性能。CACHE 选项规定了为了提高访问速度要存储多少个序列值。

要在 "Persons" 表中插入新记录，我们必须使用 nextval 函数（该函数从 seq_person 序列中取回下一个值）：

```
INSERT INTO Persons (P_Id,FirstName,LastName)
VALUES (seq_person.nextval,'Lars','Monsen')
```

上面的 SQL 语句会在 "Persons" 表中插入一条新记录。"P_Id" 的赋值是来自 seq_person 序列的下一个数字。"FirstName" 会被设置为 "Bill"，"LastName" 列会被设置为 "Gates"。

---

## SQL VIEW 视图是可视化表

---

SQL create view语句

视图：SQL中，视图是基于SQL语句的结果集的可视化表。视图包含行和列，就像一个真实的表中的字段，我们可以向视图添加SQL函数，where以及join语句，也可以提交数据，就像这些来自于某个单一的表

***注释***：数据库的设计和结构不会受到视图中的函数，where或join语句的影响

---

SQL create view

可以从某个查询内部，某个存储过程内部或者另一个视图内部来使用视图。通过向视图函数添加函数，join等等，我们可以向用户精确地提交我们希望提交的数据。

样本数据库Northwind拥有一些被默认安装的视图。视图“Current Product List”会从列表列出所有正在使用的产品。

```mysql
create view [Current product List] as
select ProductID, ProductName from Products where Doscontinued=no
```

```mysql
#查询上面这个视图
select * from [Current Product list]
```

---

```mysql
#数据库的另一个视图会选取Products表中所有单位价格高于平均单位价格的产品
create view [products above average price] as select productName, UnitPrice from Products where UnitPrice > (select avg(UnitPrice) from Products)
#视图的查询
select * from [Products above Average price]
```

---

## SQL日期

当我们处理日期时，最难的任务恐怕是确保所插入的日期的格式，与数据库中日期列的格式相匹配。

只要数据包含的只是日期部分，运行查询就不会出问题。但是，如果涉及时间，情况就有点复杂了。

在讨论日期查询的复杂性之前，我们先来看看最重要的内建日期处理函数。 MySQL Date 函数

下面的表格列出了 MySQL 中最重要的内建日期函数：

| 函数                                                         | 描述                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [NOW()](http://www.w3school.com.cn/sql/func_now.asp)         | 返回当前的日期和时间                |
| [CURDATE()](http://www.w3school.com.cn/sql/func_curdate.asp) | 返回当前的日期                      |
| [CURTIME()](http://www.w3school.com.cn/sql/func_curtime.asp) | 返回当前的时间                      |
| [DATE()](http://www.w3school.com.cn/sql/func_date.asp)       | 提取日期或日期/时间表达式的日期部分 |
| [EXTRACT()](http://www.w3school.com.cn/sql/func_extract.asp) | 返回日期/时间按的单独部分           |
| [DATE_ADD()](http://www.w3school.com.cn/sql/func_date_add.asp) | 给日期添加指定的时间间隔            |
| [DATE_SUB()](http://www.w3school.com.cn/sql/func_date_sub.asp) | 从日期减去指定的时间间隔            |
| [DATEDIFF()](http://www.w3school.com.cn/sql/func_datediff_mysql.asp) | 返回两个日期之间的天数              |
| [DATE_FORMAT()](http://www.w3school.com.cn/sql/func_date_format.asp) | 用不同的格式显示日期/时间           |

## SQL Server Date 函数

下面的表格列出了 SQL Server 中最重要的内建日期函数：

| 函数                                                         | 描述                             |
| ------------------------------------------------------------ | -------------------------------- |
| [GETDATE()](http://www.w3school.com.cn/sql/func_getdate.asp) | 返回当前日期和时间               |
| [DATEPART()](http://www.w3school.com.cn/sql/func_datepart.asp) | 返回日期/时间的单独部分          |
| [DATEADD()](http://www.w3school.com.cn/sql/func_dateadd.asp) | 在日期中添加或减去指定的时间间隔 |
| [DATEDIFF()](http://www.w3school.com.cn/sql/func_datediff.asp) | 返回两个日期之间的时间           |
| [CONVERT()](http://www.w3school.com.cn/sql/func_convert.asp) | 用不同的格式显示日期/时间        |

## SQL Date 数据类型

MySQL 使用下列数据类型在数据库中存储日期或日期/时间值：

- DATE - 格式 YYYY-MM-DD
- DATETIME - 格式: YYYY-MM-DD HH:MM:SS
- TIMESTAMP - 格式: YYYY-MM-DD HH:MM:SS
- YEAR - 格式 YYYY 或 YY

SQL Server 使用下列数据类型在数据库中存储日期或日期/时间值：

- DATE - 格式 YYYY-MM-DD
- DATETIME - 格式: YYYY-MM-DD HH:MM:SS
- SMALLDATETIME - 格式: YYYY-MM-DD HH:MM:SS
- TIMESTAMP - 格式: 唯一的数字

## SQL 日期处理

如果不涉及时间部分，那么我们可以轻松地比较两个日期！

假设我们有下面这个 "Orders" 表：

| OrderId | ProductName  | OrderDate  |
| ------- | ------------ | ---------- |
| 1       | computer     | 2008-12-26 |
| 2       | printer      | 2008-12-26 |
| 3       | electrograph | 2008-11-12 |
| 4       | telephone    | 2008-10-19 |

现在，我们希望从上表中选取 OrderDate 为 "2008-12-26" 的记录。

我们使用如下 SELECT 语句：

```
SELECT * FROM Orders WHERE OrderDate='2008-12-26'
```

结果集：

| OrderId | ProductName  | OrderDate  |
| ------- | ------------ | ---------- |
| 1       | computer     | 2008-12-26 |
| 3       | electrograph | 2008-12-26 |

现在假设 "Orders" 类似这样（请注意 "OrderDate" 列中的时间部分）：

| OrderId | ProductName  | OrderDate           |
| ------- | ------------ | ------------------- |
| 1       | computer     | 2008-12-26 16:23:55 |
| 2       | printer      | 2008-12-26 10:45:26 |
| 3       | electrograph | 2008-11-12 14:12:08 |
| 4       | telephone    | 2008-10-19 12:56:10 |

如果我们使用上面的 SELECT 语句：

```
SELECT * FROM Orders WHERE OrderDate='2008-12-26'
```

那么我们得不到结果。这是由于该查询不含有时间部分的日期。

提示：如果您希望使查询简单且更易维护，那么请不要在日期中使用时间部分！

---

## SQL NULL值

NULL是遗漏的未知数据，表的列默认可以存放NULL值。

---

IS NULL和IS NOT NULL操作符

---

如果表中某个列是可选的，那么可以在不向该列添加值得情况下插入记录或者更新已有的记录。这意味着该字段以NULL值保存。NULL的处理方式与其他值不同，NULL用作未知的或不适用的值的占位符。无法比较NULL和0，他们是不相等的。

---

无法使用=， <或者<>测试NULL值，只能使用NULL或者IS NOT NULL操作符。

请看下面的 "Persons" 表：

| Id   | LastName | FirstName | Address      | City     |
| ---- | -------- | --------- | ------------ | -------- |
| 1    | Adams    | John      |              | London   |
| 2    | Bush     | George    | Fifth Avenue | New York |
| 3    | Carter   | Thomas    |              | Beijing  |

```mysql
#测试NULL
SELECT LastName,FirstName,Address FROM Persons
WHERE Address IS NULL
#测试IS NOT NULL
SELECT LastName,FirstName,Address FROM Persons
WHERE Address IS NOT NULL
```

---

## SQL NULL函数

## SQL ISNULL()、NVL()、IFNULL() 和 COALESCE() 函数

请看下面的 "Products" 表：

| P_Id | ProductName | UnitPrice | UnitsInStock | UnitsOnOrder |
| ---- | ----------- | --------- | ------------ | ------------ |
| 1    | computer    | 699       | 25           | 15           |
| 2    | printer     | 365       | 36           |              |
| 3    | telephone   | 280       | 159          | 57           |

假如 "UnitsOnOrder" 是可选的，而且可以包含 NULL 值。

我们使用如下 SELECT 语句：

```
SELECT ProductName,UnitPrice*(UnitsInStock+UnitsOnOrder)
FROM Products
```

在上面的例子中，如果有 "UnitsOnOrder" 值是 NULL，那么结果是 NULL。

微软的 ISNULL() 函数用于规定如何处理 NULL 值。

NVL(), IFNULL() 和 COALESCE() 函数也可以达到相同的结果。

在这里，我们希望 NULL 值为 0。

下面，如果 "UnitsOnOrder" 是 NULL，则不利于计算，因此如果值是 NULL 则 ISNULL() 返回 0。

### SQL Server / MS Access

```
SELECT ProductName,UnitPrice*(UnitsInStock+ISNULL(UnitsOnOrder,0))
FROM Products
```

### Oracle

Oracle 没有 ISNULL() 函数。不过，我们可以使用 NVL() 函数达到相同的结果：

```
SELECT ProductName,UnitPrice*(UnitsInStock+NVL(UnitsOnOrder,0))
FROM Products
```

### MySQL

MySQL 也拥有类似 ISNULL() 的函数。不过它的工作方式与微软的 ISNULL() 函数有点不同。

在 MySQL 中，我们可以使用 IFNULL() 函数，就像这样：

```
SELECT ProductName,UnitPrice*(UnitsInStock+IFNULL(UnitsOnOrder,0))
FROM Products
```

或者我们可以使用 COALESCE() 函数，就像这样：

```
SELECT ProductName,UnitPrice*(UnitsInStock+COALESCE(UnitsOnOrder,0))
FROM Products
```

---SQL 数据类型

## MySQL 数据类型

在 MySQL 中，有三种主要的类型：文本、数字和日期/时间类型。

### Text 类型：

| 数据类型         | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| CHAR(size)       | 保存固定长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的长度。最多 255 个字符。 |
| VARCHAR(size)    | 保存可变长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的最大长度。最多 255 个字符。注释：如果值的长度大于 255，则被转换为 TEXT 类型。 |
| TINYTEXT         | 存放最大长度为 255 个字符的字符串。                          |
| TEXT             | 存放最大长度为 65,535 个字符的字符串。                       |
| BLOB             | 用于 BLOBs (Binary Large OBjects)。存放最多 65,535 字节的数据。 |
| MEDIUMTEXT       | 存放最大长度为 16,777,215 个字符的字符串。                   |
| MEDIUMBLOB       | 用于 BLOBs (Binary Large OBjects)。存放最多 16,777,215 字节的数据。 |
| LONGTEXT         | 存放最大长度为 4,294,967,295 个字符的字符串。                |
| LONGBLOB         | 用于 BLOBs (Binary Large OBjects)。存放最多 4,294,967,295 字节的数据。 |
| ENUM(x,y,z,etc.) | 允许你输入可能值的列表。可以在 ENUM 列表中列出最大 65535 个值。如果列表中不存在插入的值，则插入空值。注释：这些值是按照你输入的顺序存储的。可以按照此格式输入可能的值：ENUM('X','Y','Z') |
| SET              | 与 ENUM 类似，SET 最多只能包含 64 个列表项，不过 SET 可存储一个以上的值。 |

### Number 类型：

| 数据类型        | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| TINYINT(size)   | -128 到 127 常规。0 到 255 无符号*。在括号中规定最大位数。   |
| SMALLINT(size)  | -32768 到 32767 常规。0 到 65535 无符号*。在括号中规定最大位数。 |
| MEDIUMINT(size) | -8388608 到 8388607 普通。0 to 16777215 无符号*。在括号中规定最大位数。 |
| INT(size)       | -2147483648 到 2147483647 常规。0 到 4294967295 无符号*。在括号中规定最大位数。 |
| BIGINT(size)    | -9223372036854775808 到 9223372036854775807 常规。0 到 18446744073709551615 无符号*。在括号中规定最大位数。 |
| FLOAT(size,d)   | 带有浮动小数点的小数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。 |
| DOUBLE(size,d)  | 带有浮动小数点的大数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。 |
| DECIMAL(size,d) | 作为字符串存储的 DOUBLE 类型，允许固定的小数点。             |

\* 这些整数类型拥有额外的选项 UNSIGNED。通常，整数可以是负数或正数。如果添加 UNSIGNED 属性，那么范围将从 0 开始，而不是某个负数。

### Date 类型：

| 数据类型    | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| DATE()      | 日期。格式：YYYY-MM-DD注释：支持的范围是从 '1000-01-01' 到 '9999-12-31' |
| DATETIME()  | *日期和时间的组合。格式：YYYY-MM-DD HH:MM:SS注释：支持的范围是从 '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59' |
| TIMESTAMP() | *时间戳。TIMESTAMP 值使用 Unix 纪元('1970-01-01 00:00:00' UTC) 至今的描述来存储。格式：YYYY-MM-DD HH:MM:SS注释：支持的范围是从 '1970-01-01 00:00:01' UTC 到 '2038-01-09 03:14:07' UTC |
| TIME()      | 时间。格式：HH:MM:SS 注释：支持的范围是从 '-838:59:59' 到 '838:59:59' |
| YEAR()      | 2 位或 4 位格式的年。注释：4 位格式所允许的值：1901 到 2155。2 位格式所允许的值：70 到 69，表示从 1970 到 2069。 |

\* 即便 DATETIME 和 TIMESTAMP 返回相同的格式，它们的工作方式很不同。在 INSERT 或 UPDATE 查询中，TIMESTAMP 自动把自身设置为当前的日期和时间。TIMESTAMP 也接受不同的格式，比如 YYYYMMDDHHMMSS、YYMMDDHHMMSS、YYYYMMDD 或 YYMMDD。

---

## SQL 服务器

现代的SQL服务器构建在RDBMS之上

---

### DBMS -数据库管理系统（Database Management system)

数据库管理系统是一种可以访问数据库中数据的计算机程序。

DBMS使我们有能力在数据苦衷提取，修改或者存贮信息。

不同的DBMS提供不同的函数供查询，提交以及修改数据。

---

## RDBMS-关系数据库管理系统(Relational Database Management System)

关系数据库管理系统（rdbms）也是一种数据库管理系统，其数据库是根据数据间关系来组织和访问数据的。

RDBMS 是 SQL 的基础，也是所有现代数据库系统诸如 Oracle、SQL Server、IBM DB2、Sybase、MySQL 以及 Microsoft Access 的基础。 

---

# SQL 函数

内建函数的语法：

```mssql
select function(col) from table
```

函数类型：

​	Aggregate函数和Scale函数

---

合计函数(Aaggregate functions)

Aggregate函数的操作面向一系列的值，并返回单一的值。

**注释:**如果select语句的项目列表中的众多其他表达式中使用select语句，则这个select必须使用Group By语句。

Persons表:

| Name           | Age  |
| -------------- | ---- |
| Adams, John    | 38   |
| Bush, George   | 33   |
| Carter, Thomas | 28   |

### MS Access 中的合计函数

| 函数                                                         | 描述                             |
| ------------------------------------------------------------ | -------------------------------- |
| [AVG(column)](http://www.w3school.com.cn/sql/sql_func_avg.asp) | 返回某列的平均值                 |
| [COUNT(column)](http://www.w3school.com.cn/sql/sql_func_count.asp) | 返回某列的行数（不包括 NULL 值） |
| [COUNT(*)](http://www.w3school.com.cn/sql/sql_func_count_ast.asp) | 返回被选行数                     |
| FIRST(column)                                                | 返回在指定的域中第一个记录的值   |
| LAST(column)                                                 | 返回在指定的域中最后一个记录的值 |
| [MAX(column)](http://www.w3school.com.cn/sql/sql_func_max.asp) | 返回某列的最高值                 |
| [MIN(column)](http://www.w3school.com.cn/sql/sql_func_min.asp) | 返回某列的最低值                 |
| STDEV(column)                                                |                                  |
| STDEVP(column)                                               |                                  |
| [SUM(column)](http://www.w3school.com.cn/sql/sql_func_sum.asp) | 返回某列的总和                   |
| VAR(column)                                                  |                                  |
| VARP(column)                                                 |                                  |

### 在 SQL Server 中的合计函数

| 函数                                                         | 描述                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| [AVG(column)](http://www.w3school.com.cn/sql/sql_func_avg.asp) | 返回某列的平均值                                         |
| BINARY_CHECKSUM                                              |                                                          |
| CHECKSUM                                                     |                                                          |
| CHECKSUM_AGG                                                 |                                                          |
| [COUNT(column)](http://www.w3school.com.cn/sql/sql_func_count.asp) | 返回某列的行数（不包括NULL值）                           |
| [COUNT(*)](http://www.w3school.com.cn/sql/sql_func_count_ast.asp) | 返回被选行数                                             |
| [COUNT(DISTINCT column)](http://www.w3school.com.cn/sql/sql_func_count_distinct.asp) | 返回相异结果的数目                                       |
| [FIRST(column)](http://www.w3school.com.cn/sql/sql_func_first.asp) | 返回在指定的域中第一个记录的值（SQLServer2000 不支持）   |
| [LAST(column)](http://www.w3school.com.cn/sql/sql_func_last.asp) | 返回在指定的域中最后一个记录的值（SQLServer2000 不支持） |
| [MAX(column)](http://www.w3school.com.cn/sql/sql_func_max.asp) | 返回某列的最高值                                         |
| [MIN(column)](http://www.w3school.com.cn/sql/sql_func_min.asp) | 返回某列的最低值                                         |
| STDEV(column)                                                |                                                          |
| STDEVP(column)                                               |                                                          |
| [SUM(column)](http://www.w3school.com.cn/sql/sql_func_sum.asp) | 返回某列的总和                                           |
| VAR(column)                                                  |                                                          |
| VARP(column)                                                 |                                                          |

---

## Scalar函数

Scalar函数的操作面向某个单一的值，并返回输入值的一个单一的值。

### MS Access 中的 Scalar 函数

| 函数                    | 描述                                   |
| ----------------------- | -------------------------------------- |
| UCASE(c)                | 将某个域转换为大写                     |
| LCASE(c)                | 将某个域转换为小写                     |
| MID(c,start[,end])      | 从某个文本域提取字符                   |
| LEN(c)                  | 返回某个文本域的长度                   |
| INSTR(c,char)           | 返回在某个文本域中指定字符的数值位置   |
| LEFT(c,number_of_char)  | 返回某个被请求的文本域的左侧部分       |
| RIGHT(c,number_of_char) | 返回某个被请求的文本域的右侧部分       |
| ROUND(c,decimals)       | 对某个数值域进行指定小数位数的四舍五入 |
| MOD(x,y)                | 返回除法操作的余数                     |
| NOW()                   | 返回当前的系统日期                     |
| FORMAT(c,format)        | 改变某个域的显示方式                   |
| DATEDIFF(d,date1,date2) | 用于执行日期计算                       |

---

### 定义和用法

SQL AVG()用法

select avg(col) from table_name

---

 