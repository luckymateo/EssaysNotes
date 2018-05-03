#mysql锁的应用
****

> * 每一个事务都是一个单独的线程，ex:A、B、C 三个事务，A加读锁（lock table a_text read;），此时一切对表a_test的 insert update 操作都将进入锁等待，并且A事务加的读锁，只能在A事务中释放（unlock tables;）,其他事务释放锁不起作用，因为每个事务是单独的线程

> * 查看当前数据库锁请求的三种方法
	* show open tables where in_use > 0; // 查询当前锁占用的表
	* 通过 information_shcema 数据库查询
 	* mysql> show processlist;
 	
	+----+------+-----------+------+---------+------+----------+------------------+
	| Id | User | Host      | db   | Command | Time | State    | Info             |
	+----+------+-----------+------+---------+------+----------+------------------+
	|  2 | root | localhost | test | Sleep   |    7 |          | NULL             |
	|  3 | root | localhost | test | Sleep   |   74 |          | NULL             |
	|  5 | root | localhost | test | Query   |    0 | starting | show processlist |
	+----+------+-----------+------+---------+------+----------+------------------+
	3 rows in set (0.00 sec)
 	
> 	* mysql>  show full processlist \G; // full 可以不写

	*************************** 1. row ***************************
     	Id: 2
   	User: root
   	Host: localhost
     	db: test
	Command: Sleep
   	Time: 35
  	State:
   	Info: NULL
	*************************** 2. row ***************************
     	Id: 3
   	User: root
   	Host: localhost
     	db: test
	Command: Sleep
   	Time: 102
  	State:
   	Info: NULL
	*************************** 3. row ***************************
     	Id: 5
   	User: root
   	Host: localhost
     	db: test
	Command: Query
   	Time: 0
  	State: starting
   	Info: show processlist
	3 rows in set (0.00 sec)

	ERROR:
	No query specified

> * 查看当前数据库
	* select database();
	* show tables;
	* status;

> * 开启事务 start transaction  或者 begin，开启事务后，如果没有执行任何sql语句。不会生成事务ID，该事务是一个空的事务。如果执行了sql语句，通过 （SELECT TRX_ID FROM INFORMATION_SCHEMA.INNODB_TRX）这条语句可以查看到当前的事务ID
> * 对表的加锁（lock table actor write;），即使在显示开启事务后的加锁，通过rollback也无法回滚
> * 在锁表期间，用 start transaction 命令开始一个新事务，会造成一个隐含的 unlock tables 被执行
> * 在同一个事务中，最好不使用不同存储引擎的表，否则 ROLLBACK 时需要对非事 务类型的表进行特别的处理，因为 COMMIT、ROLLBACK 只能对事务类型的表进行提交和回滚。
> * savepoint test; 在事务中可以通过定义 SAVEPOINT，指定回滚事务的一个部分
> * rollback to savepoint test; 通过定义 SAVEPOINT 来指定需要 回滚的事务的位置。

##分布式事务的使用 没学会
****

###分布式事务的原理
> 
