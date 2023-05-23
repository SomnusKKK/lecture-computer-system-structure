# CH3 SQL

简述SQL语言的特点；
- 综合统一
- 高度非过程化
- 面向集合的操作方式
- 以同一种语法结构提供多种使用方式
- 语言简洁，易学易用

列出表级约束或行级约束的几个关键字，并解释其含义；
- PRIMARY KEY，主码
- FOREIGN KEY，外码
- UNIQUE，取唯一值
- NOT NULL 和 NULL 约束 
- DEFAULT 定义
- CHECK 约束

简述索引的含义，并说明索引与ORDER BY的区别；
- 索引：对表中的记录进行逻辑排序，加快检索的速度。
- 区别：索引建立好后是时时刻刻保持有序的；ORDER BY 是每次询问都重新排序，本身并不存在实际对应的表结构。

建表： CREATE TABLE<表名> ...（注意每一行末尾的','）(最后一行不加',')

写出完整的SELECT语句的格式；
``` SQL
select [all | distinct] <目标列表达式>[, <目标别表达式>] ...
from <表名或视图名>[, <表明或视图名>] | (<select 语句>) [AS] <别名>
[where <条件表达式>]
[group by <列名 1> [having <条件表达式>]]
[order by <列名 2> [ASC | DESC]];
```

说明WHERE子句中的<条件表达式>，与HAVING子句中的<组过滤表达式>的区别；P99
- where 子句与 having 短语的区别在于作用对象不同。where 子句作用域基本表或视图，从中选择满足条件的元组。having 短语作用域组，从中选择满足条件的组。

掌握关键字：DISTINCT, AS 别名,LIKE,BETWEEN AND, NULL等

给出组函数（聚集函数）与单值函数的区别。
- 聚集函数的作用对象往往是一列，而单值函数的作用对象往往是一个值。
- where 子句中是不能用聚集函数作为条件表达式的。聚集函数只能用于 select 子句和 group by 中的 having 子句。

子查询的定义：在一个查询中嵌套另一个查询

子查询注意事项；ALL, ANY ,EXISTS(子查询)的使用。

用ALTER函数的 ADD，ALTER，DROP操作修改约束

DROP函数的使用：
``` SQL
DROP TABLE<表名> [CASCADE（没有限制条件） | RESTRICT（有限制条件，默认）] ；
```

索引：
- 创建索引
``` SQL
CREATE [UNIQUE（唯一索引）] INDEX<索引名> On <索引名>（属性名）；
```
- 删除索引
``` SQL
DROP INDEX <索引名>；
```
- 对表中的记录进行逻辑排序，加快检索速度
  - 缺点：耗费磁盘空间，降低了更新操作的性能（值真实存在内存空间中）
- 三类索引
  - 普通索引
  - 唯一索引
  - 聚集索引（PRIMARY KEY 隐式创建）

数据操纵：
- Insert
  ``` SQL
  Insert into <表> [VALUES()| Select ...];
  ``` 
- Update：
  ``` SQL
  update <表> set <列名> = <表达式> [where];
  ``` 
- Delete:  
  ``` SQL
  Delete from <表> [where];
  ``` 
视图：
- 从一个或几个基本表导出的表（数据库只存储视图的定义，不存放视图对应的数据）
- 创建
  ``` SQL
  Create view <视图名>[(属性名)--虚列] As [where];
  ``` 
- 删除
  ``` SQL
  Drop view <视图名>;
  ``` 
视图的作用；
- 视图能够简化用户的操作
- 视图使用户能以多种角度看待同一数据
- 视图对重构数据库提供了一定程度的逻辑独立性
- 视图能够对机密数据提供安全保护
- 适当利用视图可以更清晰地表达查询

视图的更新问题。
- 由于视图时不实际存储数据的虚表，因此对视图的更新最终要转换为对基本表的更新。
- 在关系数据库中，并不是所有的视图都是可更新的。一般地，行列子集视图是可更新的。

表示今天：WHERE REGIST_DATE=GETDATE().
