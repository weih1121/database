SQL SELECT语句

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

select distinct 返回唯一不同的值

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

where子句规定选择的标准

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

and & or用于基于一个以上的条件对记录进行过滤

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