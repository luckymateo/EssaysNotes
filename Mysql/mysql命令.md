

#mysql
****

#DDL 语句
##	1. mysql.server start  启动mysql服务
##    2. mysql -h localhost -P 3306 -u root -p -D test (-h 域名 -P端口 -u用户名 -p密码 -D使用的数据库)
##    3. show databases; 列出所有数据库
##    4. create database test; 创建数据库
##    5. drop database test; 删除数据库
##    6. use test; 使用该数据库
##    7. show tables; 展示该数据库中所有的表
##    8. create table emp(ename varchar(10),hiredate date,sal decimal(10,2),deptno int(2)); 创建一张表出来
##    9. mysql> desc emp; 展示表信息
	+----------+---------------+------+-----+---------+-------+
	| Field    | Type          | Null | Key | Default | Extra |
	+----------+---------------+------+-----+---------+-------+
	| ename    | varchar(10)   | YES  |     | NULL    |       |
	| hiredate | date          | YES  |     | NULL    |       |
	| sal      | decimal(10,2) | YES  |     | NULL    |       |
	| deptno   | int(2)        | YES  |     | NULL    |       |
	+----------+---------------+------+-----+---------+-------+
	4 rows in set (0.00 sec)
##    10. mysql> show create table emp \G;
	*************************** 1. row ***************************
       Table: emp
	Create Table: CREATE TABLE `emp` (
  		`ename` varchar(10) DEFAULT NULL,
 	 	`hiredate` date DEFAULT NULL,
  		`sal` decimal(10,2) DEFAULT NULL,
  		`deptno` int(2) DEFAULT NULL
	) ENGINE=InnoDB DEFAULT CHARSET=utf8
	1 row in set (0.00 sec)
##    11. drop table emp; 删除表
##    12. alter table emp modify ename varchar(20); 修改表字段
##    13. alter table emp add column age int(3); 增加年龄字段
##    14. alter table emp drop column age; 删除表字段
##    15. alter table emp change age age1 int(4); 修改字段名称
##    16. alter table emp add birth date after ename; 修改表字段的顺序
##    17. alter table emp modify age int(3) first; 修改字段 age，将它放在最前面
##    18. alter table emp rename emp1; 修改表名

#DML 语句
##    19. insert into emp values('lisa','2003-02-01','3000',2); 插入语句
##    20. insert into emp (ename,sal) values('dony',1000);只对表中的 ename 和 sal 字段显式插入值
##    21. update emp set sal=4000 where ename='lisa'; 更新表中数据
##    22. update emp a,dept b set a.sal=a.sal*b.deptno,b.deptname=a.ename where a.deptno=b.deptno;连表查询
##    23. delete from emp where ename='dony'; 删除某一行记录
##    24. select distinct deptno from emp;查询不重复的记录
> `where 后面的条件是一个字段的‘=’ 比较，除了‘=’外，还可以使用>、<、>=、<=、!=等比较运算符;多个条件之间还可以使 用 or、and 等逻辑运算符进行多条件联合查询`

##    25. select * from emp where deptno=1;条件查询
	+-------+------------+---------+--------+
	| ename | hiredate   | sal     | deptno |
	+-------+------------+---------+--------+
	| zzx1  | 2000-01-01 | 2000.00 |      1 |
	| test  | 2004-05-20 | 5000.00 |      1 |
	+-------+------------+---------+--------+
##    26. select * from emp where deptno=1 and sal<3000;
	+-------+------------+---------+--------+
	| ename | hiredate   | sal     | deptno |
	+-------+------------+---------+--------+
	| zzx1  | 2000-01-01 | 2000.00 |      1 |
	+-------+------------+---------+--------+
##    27. select * from emp order by deptno,sal desc;  DESC 和 ASC 是排序顺序关键字，DESC 表示按照字段进行降序排列，ASC 则表示升序 排列，如果不写此关键字默认是升序排列。ORDER BY 后面可以跟多个不同的排序字段，并 且每个排序字段可以有不同的排序顺序。
##    28. select * from emp order by sal desc limit 3; emp 表中按照 sal 排序后从第二条记录开始，显示 3 条记录:

##聚合
* 聚合:having 和 where 的区别在于 having 是对聚合后的结果进行条件的过滤，而 where 是在聚 合前就对记录进行过滤，如果逻辑允许，我们尽可能用 where 先过滤记录，这样因为结果 集减小，将对聚合的效率大大提高，最后再根据逻辑看是否用 having 进行再过滤。
* 聚合操作，也就是聚合函数，常用的有 sum(求和)、count(*)(记 录数)、max(最大值)、min(最小值)。
* GROUP BY 关键字表示要进行分类聚合的字段，比如要按照部门分类统计员工数量，部门 就应该写在 group by 后面。
* WITH ROLLUP 是可选语法，表明是否对分类聚合后的结果进行再汇总。
* HAVING 关键字表示对分类后的结果再进行条件的过滤。

##    29. select deptno,count(1) from emp group by deptno; 分类统计数量
##    30. mysql> select deptno,count(1) from emp group by deptno with rollup; 既要统计各部门人数，又要统计总人数:
	+--------+----------+
	| deptno | count(1) |
	+--------+----------+
	|      1 |        2 |
	|      2 |        1 |
	|      4 |        1 |
	|   NULL |        4 |
	+--------+----------+
4 rows in set (0.00 sec)
##    31. select deptno,count(1) from emp group by deptno having count(1)>1; 统计人数大于 1 人的部门:
	+--------+----------+
	| deptno | count(1) |
	+--------+----------+
	|      1 |        2 |
	+--------+----------+
	1 row in set (0.00 sec)
##    32. mysql> select sum(sal),max(sal),min(sal) from emp; 统计公司所有员工的薪水总额、最高和最低薪水:
	+----------+----------+----------+
	| sum(sal) | max(sal) | min(sal) |
	+----------+----------+----------+
	| 19000.00 |  8000.00 |  2000.00 |
	+----------+----------+----------+
	1 row in set (0.00 sec)

## 表连接
* 当需要同时显示多个表中的字段时，就可以用表连接来实现这样的功能。 从大类上分，表连接分为内连接和外连接，它们之间的最主要区别是內连接仅选出两张表中 互相匹配的记录，而外连接会选出其他不匹配的记录。我们最常用的是内连接。
* 外连接有分为左连接和右连接，具体定义如下。
	* 左连接:包含所有的左边表中的记录甚至是右边表中没有和它匹配的记录
	* 右连接:包含所有的右边表中的记录甚至是左边表中没有和它匹配的记录


##    33. mysql> select ename,deptname from emp,dept where emp.deptno=dept.deptno;
	+--------+----------+
	| ename  | deptname |
	+--------+----------+
	| zzx1   | tech     |
	| lisa   | sale     |
	| test   | tech     |
	| bzshen | net      |
	| go_nil | hr       |
	+--------+----------+
	5 rows in set (0.00 sec)
	
	
	mysql> select ename,deptname from emp left join dept on emp.deptno=dept.deptno;  左外连接，会将不存在的也展示出来（可以改写为右外连接  select ename,deptname from dept right join emp on dept.deptno=emp.deptno;）
	+-----------+----------+
	| ename     | deptname |
	+-----------+----------+
	| zzx1      | tech     |
	| test      | tech     |
	| lisa      | sale     |
	| go_nil    | hr       |
	| bzshen    | net      |
	| Java_null | NULL     |
	+-----------+----------+
	6 rows in set (0.00 sec)
##    34. select * from emp where deptno in(select deptno from dept); 子查询
##    35. select emp.* from emp ,dept where emp.deptno=dept.deptno; 某些情况子查询可以转换为表连接
## 记录联合
* UNION 和 UNION ALL 的主要区别是 UNION ALL 是把结果集直接合并在一起，而 UNION 是将 UNION ALL 后的结果进行一次 DISTINCT，去除重复记录后的结果。
* ss
 
##    36. mysql> select deptno from emp union all select deptno from dept;
	+--------+
	| deptno |
	+--------+
	|      1 |
	|      2 |
	|      1 |
	|      4 |
	|      3 |
	|      5 |
	|      1 |
	|      2 |
	|      3 |
	|      4 |
	+--------+
	10 rows in set (0.01 sec)
##    37. mysql> select deptno from emp union select deptno from dept;
	+--------+
	| deptno |
	+--------+
	|      1 |
	|      2 |
	|      4 |
	|      3 |
	|      5 |
	+--------+
	5 rows in set (0.00 sec)
## DCL  开发人员一般不去使用
##    38.  mysql> select 0 is null, null is null; “IS NULL”运算符的使用格式为“a IS NULL”,当 a 的值为 NULL，则返回值为 1，否则 返回 0。
	+-----------+--------------+
	| 0 is null | null is null | 
	+-----------+--------------+ 
	| 0 | 1 | 
	+-----------+--------------+ 
	1 row in set (0.02 sec)
##    39. mysql> select 0 is not null, null is not null; “IS NOT NULL”运算符的使用格式为“a IS NOT NULL”。和“IS NULL”相反，当 a 的 值不为 NULL，则返回值为 1，否则返回 0。
	+----------------+-------------------+
	| 0 is not null | null is not null | 
	+----------------+-------------------+ 
	|1|0| 
	+----------------+-------------------+
1 row in set (0.00 sec)
##    40. select 123456 like '123%',123456 like '%123%',123456 like '%321%';  《“LIKE”运算符的使用格式为“a LIKE %123%”,当 a 中含有字符串“123”时，则返回 值为 1，否则返回 0。》
##    41. mysql> select 'abcdef' regexp 'ab' ,'abcdefg' regexp 'k'; “REGEXP”运算符的使用格式为“str REGEXP str_pat”,当 str 字符串中含有 str_pat 相匹配的字符串时，则返回值为 1，否则返回 0
	+----------------------+----------------------+
	| 'abcdef' regexp 'ab' | 'abcdefg' regexp 'k' |
	+----------------------+----------------------+
	|                    1 |                    0 |
	+----------------------+----------------------+
	1 row in set (0.00 sec)


