## 一、数据类型

1. 显示宽度只用于显示，并不能限制取
2. 浮点数相对于定点数的优点是在长度一定的情况下，浮点数能够表示更大的数据范围；缺点是会引起精度问题，尽量避免做浮点数比较
3. float(5, 2)    宽度5 ，保留2位小数
4. ENUM类型的字段只能从定义的列值中选择一个值插入，而SET类型的列可从定义的列值中选择多个字符的联合

- 选择最小的可用类型，如果值永远不超过127，则使用TINYINT比INT强；
-  对于完全都是数字的，可以选择整数类型；
- 从速度方面考虑，要选择固定的列，可以使用CHAR(0-255)类型 要节省空间，使用动态的列，VARCHAR(0-255)类型；
- 要将列中的内容限制在一种选择，使用ENUM类型；
- 允许一个列中有对于一个的条目，可以使用SET类型；   

| 类型名称         | 存储需求 | 说明           |
| ---------------- | -------- | -------------- |
| tinyint(4)       | 1 Byte   | 很小的整数     |
| smallint(6)      | 2 Byte   | 小的整数       |
| mediumint(9)     | 3 Byte   | 中等大小的整数 |
| int(integer)(11) | 4 Byte   | 普通大小的整数 |
| bigint(20)       | 8 Byte   | 大整数         |
| float            | 4 Byte   |                |
| double           | 8 Byte   |                |

> 日期

- datetime默认null
- timestamp 默认当前系统时间，最大2038-1-19

| 类型名称  | 日期格式            | 日期范围              | 存储需求 |
| --------- | ------------------- | --------------------- | -------- |
| year      | YYYY                | 1901-2155             | 1 Byte   |
| time      | HH:MM:SS            | -838:59:59-838:59:59  | 3 Byte   |
| date      | YYYY-MM-DD          | 1000-01-01- 9999-12-3 | 3 Byte   |
| datetime  | YYYY-MM-DD HH:MM:SS |                       | 8 Byte   |
| timestamp |                     |                       | 4 Byte   |

> 文本字符串类型

- char和varchar
    - char(n) 固定长度，最大长度255，效率高；
    - varchar(n) 可变长度，最大长度255；
    - text(n)   可变长度，最大长度65535；

| 类型名称   | 存储需求                                   | 说明            |
| ---------- | ------------------------------------------ | --------------- |
| char(M)    | 固定长度非二进制字符串                     | M字节 1<=M<=255 |
| varchar(M) | 变长非二进制字符串                         |                 |
| tinytext   |                                            |                 |
| text       | 小的非二进制字符串                         |                 |
| mediumtext |                                            |                 |
| longtext   |                                            |                 |
| enum       | 枚举类型，只能有一个枚举字符串值           |                 |
| set        | 一个设置，字符串对象可以有0个或多个set成员 |                 |

.....

数据模型三要素：

1. 数据结构
2. 数据操作
3. 完整性约束



## 二、存储引擎

### 1. 分类

1. innoDB
    - 唯一支持事务的标准MySQL存储引擎，常用于管理敏感数据；
2. MYISAM
3. MEMORY



### 2. 设置存储引擎

1. 通过配置文件my.ini 

    ```mysql
    default-storage-engine=innodb;
    ```

2. mysql命令行中执行

    ```mysql
    set default_storage_engine=InnoDB;
    ```

3. 创建表时指定

    ```mysql
    create table stu(...) engine=innodb;
    alter table stu engine=innodb;
    ```

    



## 三、数据库

### 1. 连接数据库

```mysql
net start mysql 					# windows开启MySQL服务

net stop mysql						# windows关闭MySQL服务

mysql -h 127.0.0.1 -uroot -p		# 连接MySQL服务

mysqladmin -uroot -p oldpwd	password	newpwd		# 修改用户密码

set password=password('123');		# 修改密码为123
```



### 2. 操作数据库

```mysql
show databases;					# 显示所有数据库

use student;					# 进入student数据库

create database blogdb character set utf8;   # 创建数据库并指定字符编码集

drop database (if exists) student;			# 删除student数据库

select database();				# 显示当前连接数据库

select version();				# 显示当前MySQL版本

select now();					# 显示当前时间

select user();					# 显示当前用户

show create database blogdb;      # 查看数据库详情

show engines \G					# 显示DBMS（数据库管理系统）支持的存储引擎

show variables like '%storage_engine%';			# 查看默认存储引擎

show variables like 'character%';				# 查看当前数据库编码格式
```



## 四、数据表

1. auto_increment

- 被约束的字段自动增加，一个数据表中只能有一个字段使用该约束，该字段数据类型必须是==整形==，设置后该字段会生成唯一的ID，因此该字段也经常会被设置为PK主键，默认情况下该字段的值从1开始增加，每增加一条记录，该字段的值就+1；

- 修改自增列的起始值：alter table stu auto_increment=3;

2. PK(primary key)主键

- 一张表只能定义一个主键，实体是一个数据对象，一个实体就是一条记录；
- 一张表只能创建一个主键，但可以定义若干个候选键；

3. FK(foreign key)外键

- 在具体设置时，子表中的外键字段的数据类型必须和附表中所参考的字段的数据类型一致；

### 1. 表操作

```mysql
desc student;					# 查看student表结构/也用于检验表是否存在

show tables;		# 显示当前数据库中所有表

show create table student \G;	# 查看详细表结构

/*
* 删除表（默认restrict）
* restrict 欲删除表则不能被其他表的约束所引用如：check，foreign key等；不能有视图、触发器、存储过程及函数
* cascade 在删除本表的同时，相关的依赖对象，如视图都将被一起删除
*/
drop table student [restrict|cascade];

rename table student to stu;		# 修改表名

alter table student rename (to) stu;			# 修改表名称

alter table student comment '学生表';			  # 修改表注释

alter table student engine=innodb;				# 修改存储引擎
```



### 2. 创建表

> cascade：从父表删除或更新且自动删除或更新子表中的行；

```mysql
create table Student
(
    Sno     char(10) primary key ,
    Sname   char(20) unique comment '学生姓名',
    Sgender char(2),
    Sage    smallint,
    Sdept   char(20) comment '所在系',
    index index_Sname (Sname)     # 为创建Sname创建索引
) engine = innodb
  default charset = utf8 
  comment '学生表';

create table Course
(
    Cno     char(4) primary key,
    Cname   char(40) not null,
    Cpno    char(4) comment '先修课程',
    Ccredit smallint default 0,
    foreign key (Cpno) references Course (Cno) on delete cascade
) engine = innodb
  default charset = utf8
    comment '课程表';

create table SC
(
    Sno   char(10) comment '外键',
    Cno   char(4) comment '外键',
    Grade smallint,
    primary key (Sno, Cno),
    foreign key (Sno) references student (Sno),
    foreign key (Cno) references course (Cno)
) engine = innodb
  default charset = utf8;
  
  
create table message(
	id int primary key auto_increment,
	dt timestamp not null default  current_timestamp
);
```



### 3. 修改字段

> alter table ... 语句允许指定多个动作，用逗号分隔；

```mysql
alter table student add 字段名 字段类型 first|after 字段名;		# 添加字段（该字段设为第一个）

alter table student add unique(sage);			    # 为age字段添加unique约束

alter table student drop unique|index sage;			# 删除age字段的unique约束

alter table student add index index_name(sname);	# 添加index索引约束

alter table student drop sage;					    # 删除student表中age字段

alter table student modify sage int;				# 将age字段类型修改为int

alter table student modify sage int first|after sname;	# 修改字段顺序 1

alter table student change sage int first|after sname;	# 修改字段顺序 2

alter table student modify sage int not null;		# 添加not null约束

alter table student modify sage int;				# 删除not null约束

alter table student modify sage int default '年龄';	# 添加默认约束

alter table student modify sage int;	# 删除默认约束

alter table student change 旧字段名 新字段名 旧字段类型;		# 修改字段名称

alter table student change 旧字段名 新字段名 新字段类型;		# 字段名称和类型一同修改

alter table student modify COLUMN sname VARCHAR(100) COMMENT '姓名';	# 修改列注释

# 添加外键约束
alter table student add foreign key(sno) references course(cno);
alter table student drop foreign key fk_sno;
```



### 4. 更新数据

​		ignore关键字 如果用UPDATE语句更新多行，并且在更新这些行中的一行或多行时出现一个错误，则整个UPDATE操作被取消（错误发生前更新的所有行被恢复到它们原来的值）。

​		即使是发生错误，也继续进行更新，可使用IGNORE关键字，如下所示：UPDATE IGNORE customers…



如果想从表中删除所有行，不要使用DELETE。可使用TRUNCATE TABLE语句，它完成相同的工作，但速度更快（TRUNCATE实际是删除原来的表并重新创建一个表，而不是逐行删除表中的数据）。

```mysql
delete from student where id = 3;		# 删除指定数据

delete from student;		# 删除student表所有记录

truncate table student;

insert into student(no, name, gender) values('100012','李晓明','男'),('','','');	# 插入数据

update student set name = '李小明' where id = 1;		# 修改数据
```



### 5. 数据查询

#### 5.1 执行顺序

>    （4）select [all|distinct] <目标列表达式>...
>
>    （1）from <表名或视图名> | (<select 语句>) 
>
>    （2）[where <条件表达式>]
>
>    （3）[group by <列名1> [having <条件表达式>]]
>
>    （5）[order by <列名2> [ASC | DESC]];
>
>    （6） limit
>
>    `注：序号为执行顺序`

#### 5.2 查询条件

> where 和 having 区别：

- 唯一的差别是WHERE过滤行，而HAVING过滤分组；

| 查询条件 | 谓词                                                         |
| -------- | ------------------------------------------------------------ |
| 比较     | =，>，<，<=，>=，!=, <>(不等于)，!>，!<；not + 上述比较运算符 |
| 确定范围 | between and，not between and（闭区间）                       |
| 确定集合 | in，not in                                                   |
| 字符匹配 | like，not like                                               |
| 空值     | is null，is not null                                         |
| 多重条件 | and，or，not                                                 |
|          | distinct                                                     |
|          | exists()、any()、all()                                       |



#### 5.3 分页查询

```mysql
# 第一页 ,每页显示5条数据
select * from student limit 0, 5;

# 第二页
select * from student limit 5, 5;

# 第三页
select * from student limit 10, 5;

# 第n页，每页显示m个
select * from student limit (n-1)*m, m;
```



#### 5.4 模糊查询

> 如果查询的字符串本身含有通配符 % 或 _ ，这是需要使用escape '<换码字符>' 短语对通配符进行转义

```mysql
select * from student where name [not] like '李_';

select * from student where name [not] like '%李%';

# 查询课程名以“DB_”开头的课程情况
select * from course where cname like 'DB/_%' escape '/';
```



#### 5.5 连接查询

1. inner join 等值连接（内连接）

    > 获取两个表中字段匹配关系的记录

    ![img](https://www.runoob.com/wp-content/uploads/2014/03/img_innerjoin.gif)

    ```mysql
    select *from student s inner join sc on s.sno = sc.sno;
    # 等价于
    select *from student s, sc where s.sno = sc.sno;
    ```

2. left join 左连接

    > 获取左表所有记录，即使右表没有对应匹配的记录

    ![img](https://www.runoob.com/wp-content/uploads/2014/03/img_leftjoin.gif)

    ```mysql
    select *from student s left join sc on s.sno = sc.sno;
    ```

3. right join 右连接

    > 获取右表所有记录，即使左表没有对应匹配的记录

    ![img](https://www.runoob.com/wp-content/uploads/2014/03/img_rightjoin.gif)

    ```mysql
    select *from student s right join sc on s.sno = sc.sno;
    ```

4. 自连接（需要取别名）

    ```mysql
    # 查询员工信息和他的主管姓名
    select a.*, b.ename
    from emp a,
         emp b
    where a.empno = b.mgr;
    ```

    

#### 5.6 子查询

```mysql
select * from stu where exists(select * from person where id=1);
select * from stu where age < any(select age from person);
select * from stu where age >= all(select age from person);
```



#### 5.7 排序

```mysql
# 默认升序
select * from student order by age asc;

# 降序排序
select * from student order by age, name desc;

select * from student where age [not] between 20 and 23;
select * from student where age [not] in (19, 20, 23);
```



#### 5.8 分组查询

​		聚合函数只能查询出一行数据，但是如果想要查询除多行的聚合结果，比如查询每个部门的工资总和，就需要分组查询了。

​		where 后面只能写普通字段的条件，不能写聚合函数的条件。having结合分组查询group by使用，在having后面写聚合函数的条件。

```mysql
# 查询每个部门的平均工资大于2000的平均工资
select deptno, avg(sal) from employee group by deptno having avg(sal)>2000;

# 查询每种工作人数只查询人数为1的
select job, count(*) c from employee group by job having c=1;

# 查询每个部门工资大于1000的员工人数，按照人数升序排序
select deptno,count(*) c from emp where sal>1000 group by deptno order by c;

# 查询所有员工信息，按照部门编号升序排序，如果部门标号一致则按工资降序排序
select * from emp order by deptno asc,sal desc;

select * from emp where sal>(select avg(sal) from emp where deptno=1));
```





#### 5.9 合并查询结果

​		UNION中的每个查询必须包含相同的列、表达式或聚集函数（不过各个列不需要以相同的次序列出）。 列数据类型必须兼容：类型不必完全相同，但必须是DBMS可以隐含地转换的类型（例如，不同的数值类型或不同的日期类型）。

- union ：将所有的查询结果合并到译器，然后去重；
- union all  :  不去重

```mysql
select name from stu
union 
select name from stu_copy;

select name from stu
union all
select name from stu_copy;
```



### 6. 聚集函数

​		聚集函数运行在行组上，计算和返回单个值的函数。

- 聚集函数只能用于where子句和group by 中的having子句；

- 聚合函数的结果只根据选定行中非NULL的值进行计算，NULL值将被忽略；

- 使用聚合函数后不能查询其他列（分组查询除外）；



1. count([distinct|all] <列名>)
2. sum([distinct|all] <列名>)
3. avg([distinct|all] <列名>)
4. max([distinct|all] <列名>)
5. min([distinct|all] <列名>)

```mysql
# 查询学生总人数
select count(*) from student;

# 查询选修 1 号课程的学生平均成绩
select avg(grade) from sc where cno = 1;

# 查询各个课程号及选课人数
select cno [as] 课程号, count(sno) [as] 选课人数 from sc group by cno;

# 查询选修了3门以上课程的学生学号
select sno from sc group by sno having count(*) > 3;
```



### 7. 正则匹配

```mysql
# 1. 基本字符匹配
select name from stu where name regexp '丽';

# 2. or匹配
select name from stu where name regexp '丽|婉';

# 3. 匹配范围 [a-z] [0-9]等, [^123]表示除了123
select name from stu where name regexp '[1-5] Ton';

# 4. 匹配特殊字符
select name from stu where name regexp '\\.'; # 匹配名字中有.的
```



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220225154247537.png" alt="image-20220225154247537" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220225154331469.png" alt="image-20220225154331469" style="zoom:80%;" />

```mysql
# 
select name from stu where name regexp '[[:digit:]]{4}';
```



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220225154634459.png" alt="image-20220225154634459" style="zoom:80%;" />

```mysql
# 以一个数（包括以小数点开始的数）开始的所有产品
select name from products where name regexp '^[0-9\\.]';
```







## 五、索引

### 1. 概述

> 一个索引包含表中按照一定顺序排序的一列或多列字段，创建索引可以提高查询速度，但过多的创建则会占据许多磁盘空间；
>
> 向有索引的表中插入记录时，数据库系统会按照索引进行排序，所以可以将索引删除后再插入数据，插入后再重建索引；
>
> 所有存储引擎对每个表至少支持16个索引，总索引长度至少256B；

- 一般以下几种情况适合创建索引：
    1. 经常被查询的字段，即在where子句中出现的字段
    2. 在分组的字段，即在group by子句中出现的字段
    3. 存在依赖关系的子表与附表之间的联合查询，即主键和外键字段
    4. 设置唯一完整性约束的字段
- 一般下列情况，不适合创建索引
    1. 在查询中==很少==被使用的字段
    2. 拥有许多==重复值==的字段

### 2. 创建索引

> create [unique] index <索引名> on <表名> (<列名>[<次序>],<列名>[次序]...);

```mysql
# 1. 
create unique index stu_age on stu(sname ASC);

# 2. 
alter table student add index index_name(sname);

# 3.
create table test(
    sno int,
    index index_sno (sno)
);
```

### 3. 查看索引

```mysql
show index from stu;
# 或
show keys from t;	# mysql中索引也被称作keys
```



### 3. 修改索引

> alter index <旧索引名称> rename to <新索引名称>;

```mysql
# 重命名索引
alter index stu_age rename to index_stu_age;	

# 删除索引
drop index 索引名 on 表名; 

# 或
alter table 表名 drop index 索引名;
```



## 六、常用函数

### 1. 数值函数

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220225160801400.png" alt="image-20220225160801400" style="zoom:80%;" />

```mysql
select Round(Sqrt(age), 1) '年龄平方根' from stu;
select Floor(price) from book;
# 
select truncate(28.55, 1);	# 28.5
select truncate(28.55, -1);	# 20
select mod(11, 2);	# 1
```



### 2. 字符函数

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220225155834742.png" alt="image-20220225155834742" style="zoom:80%;" />

```mysql
select Concat(name, '(', age, ')') '姓名(年龄)' from stu;
#
select concat('hello', ' MySQL');	# hello MySQL
select concat_ws('=', 'hello', ' MySQL');	# hello=MySQL
select lower('HELLO');	# hello
select upper('hello');	# HELLO
select length('hello');	# 5
select ltrim(' hello');
select rtrim('hello ');
select trim(' hello');
select subString('字符串', '起始位置', '长度');
select left('helloworld', 3);	# hel
select right('helloworld', 3);	# rld
select replace('字符串', 'oldstr', 'newstr');
```

### 3. 日期函数

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220225161411519.png" alt="image-20220225161411519" style="zoom:80%;" />

```mysql
# Date(birthday)指示MySQL仅提取列的日期部分
# 查询出生日期为1998-5-21 的人
select name from users where Date(birthday) = '1998-5-21';

# 检索出2005年9月下的所有订单
# 1. 
select orderName from orders where Date(orderDate) between '2005-9-1' and '2005-9-30';
# 2. 
select orderName from orders where Year(orderDate)=2005 and Month(orderDate)=9;

# 从datatime中提取时间分量
select extract(year from now());
select extract(month from now());
select extract(day from now());
select extract(hour from now());
select extract(minute from now());
select extract(second from now());

#
select name, extract(year from 入职时间) from emp;
```



### 4. 加密函数

```mysql
select md5(123);	#  202cb962ac59075b964b07152d234b70
select password(123);	# *23AE809DDACAF96AF0FD78ED04B6A265E05AA257
```

### 5. ifnull()

> ifnull(x, y) ; 
>
> age = ifnull(x, y)      如果x值为null  则 age = y,  否则age=x;

```mysql
# 修年龄为null 的值为0，不为null的则不变
update emp set age = ifnull(age, 0);
```





## 七、触发器

## 七、事务

> begin;  # 开启事务
>
> rollback; # 回滚
>
> commit;  # 提交

### 1. 什么是事务？

​		通过确保成批的SQL操作要么完全执行，要么完全不执行，来维护数据库的完整性。

### 2. 事务的特点？

1. 原子性
2. 一致性
3. 隔离性：多个事务再同时执行时，能一定程度上保证互不影响；
4. 持久性：事务一旦提交，数据最终会保存再数据库中（即保存在磁盘上）

### 3. 事务的隔离级别

1. 读取未提交：一个事务可以读取到另一个事务尚未提交的数据。该隔离级别可能会产生“脏读”、“不可重复读取”、“幻影读取” 的问题。

    ![image-20220618224736802](https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220618224736802.png)

    

2. 读已提交：一个事务只能读取另外一个事务已经提交的数据。该隔离级别解决了“脏读”，但为解决：“不可重复读取”、“幻影读取” 的问题。

    ![image-20220618225931437](https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220618225931437.png)

    

3. 可重复读取：在同一个事务中，多次读取一个数据的结果一样。该隔离级别解决了“脏读”和“不可重复读取”问题，但未解决“幻影读取”的问题。

    ![image-20220618230723513](https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220618230723513.png)

    

4. 序列化：多个事务串行执行。该隔离级别解决了“脏读”、“不可重复读”、“幻影读取”问题。

事务的隔离级别越高，其并发性越低。



## 八、存储过程和存储函数

### 1. 存储过程

​		存储过程是SQL语句和流程控制语句的预编译集合，并以一个名称存储并作为一个单元进行处理（执行效率比SQL语句高）；

MySQL支持IN（传递给存储过程）、OUT（从存储过程传出，如这里所用）和INOUT（对存储过程传入和传出）类型的参数。存储过程的代码位于BEGIN和END语句内，如前所见，它们是一系列SELECT语句，用来检索值，然后保存到相应的变量（通过指定INTO关键字）。

```mysql
# 语法结构
create procedure 过程名([in|out|inout] 参数名 数据类型, ...) [特性...]
begin
	过程体
end

# 调用存储过程
call 过程名();

# 删除
drop procedure [if exists] 过程名;
```

示例

```mysql
create procedure procedure1(out a decimal(8,2), out b decimal(8,2), out c decimal(8,2))
begin
select avg(salary) into a from emp;
select max(salary) into b from emp;
select min(salary) into c from emp;
end;

# 调用
call procedure1(@salA, @salB, @salC); # 定义三个变量接收返回的值

# 显示
select @salA, @salB, @salC;
```



### 2.存储函数

```mysql
# 语法结构
create function 函数名([参数名 数据类型, ...]) returns 返回类型
begin
	过程体
end
```



### 3. 过程和函数的区别

1. 功能上
    - 存储过程：一般来说，存储过程实现的功能要复杂一点，功能强大，可以执行包括修改表等一系列数据库操作；
    - 存储函数实现的功能针对性能比较强；

2. 参数
    - 存储过程的参数类型有三种：in、out、inout；
    - 存储函数参数只有一种类似与in ；

3. 返回值
    - 存储过程声明时不需要指定返回类型；
    - 存储函数声明时需要指定返回类型，且再函数体中必须包含一个有效的return 语句；



## 九、备份

### 1. 备份数据库

```shell
# 备份整个数据库
mysqldump -u root -h host -p dbname  >  backdb.sql

# 备份数据库中特定表
mysqldump -u root -h host -p dbname tbname1, tbname2  >  backdb.sql

# 备份多个数据库
mysqldump -u root -h host -p --databases dbname1, daname2 > backdb.sql 

# 备份系统中所有数据库
mysqldump -u root -h host -p --all-databases > backdb.sql 
```



### 2. 恢复数据

```shell
# mysql命令导入sql文件还原
source D:/backup.sql;  #（需提前选择数据库）  
```

​                             



## 十、用户权限管理

### 1. 用户管理

#### 1.1 分类

- 用户
    - root（拥有所有权限）
    - 普通用户（拥有被授予的权限）

#### 1.2 创建用户

```mysql
# 创建用户并指定密码
create user '用户名'@'localhost' identified by '密码';

# 创建用户的同时授予权限
grant 权限 on table 表名 to 
```



#### 1.3 删除用户

```mysql
drop user '用户名'@'localhost';

delete from mysql.user where host='localhost' and user='用户名';
```





### 2. 权限管理

#### 2.1 常见操作权限

​		execute、drop、add、

| 对象   | 对象类型 | 操作权限                                                     |
| ------ | -------- | ------------------------------------------------------------ |
| 属性列 | column   | select、insert、update、delete、all privileges(4种权限和)    |
| 视图   | view     | select、insert、update、delete、all privileges(4种权限和)    |
| 基本表 | table    | select、insert、update、delete、alter、index、all privileges(6种权限和) |
| 数据库 | database | createtab(创建表的权限)                                      |



#### 2.2 授权

```mysql
# 查看用户权限 （usage on *.* 表示任意数据库和任意表上对任何东西没有权限）
# GRANT USAGE ON *.* TO `liqiju`@`localhost` 
show grants for '用户名'@'localhost';

# 权限 on 数据库.表 to
grant 权限 on *.* to '用户名'@'localhost';
flush privileges;	# 刷新权限列表
```



#### 2.3 收回权限

```mysql
revoke 权限 on *.* from '用户名'@'localhost';
flush privileges;
```





## 十一、性能优化



```mysql
show status like 'value';			# 查看数据库的性能
show status like 'connections';		# 连接次数
show status like 'uptime';			# MySQL数据库上线时间
show status like 'slow_queries';	# 慢查询次数
show status like 'com_select';		# 查询操作的次数
show status like 'com_insert';		# 插入操作的次数
show status like 'com_delete';		# 删除操作的次数
```

### 1. 设置索引

### 2. 优化查询

​		关于MySQL是如何执行SQL语句的，相关信息可以用explain语句来查看，可以查看的执行过程有：select,insert,update,delete等。

```mysql
explain select *from stu;		# 分析查询语句
```

返回值解释：

​		通过type、possible_keys 和 key 三个字段，就知道查询语句是否使用了索引和使用了那个索引。

| 字段          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| id            | SQL语句标识符，如果仅包含一个表的简单查询id始终为1；如果查询是多表连接查询，id按照顺便往下排 |
| select_type   | 查询类型（例：SIMPLE是简单查询，不包括子查询或union）        |
| table         | 查询的表名                                                   |
| partitions    | 表分区，非分区表始终为NULL                                   |
| type          | 语句中表对象间得连接类型。all：代表使用低效的全表扫描方式；const: 代表仅有一行匹配的结果记录；range: 代表使用了索引范围查找； |
| possible_keys | 执行时有可能用到的索引名称                                   |
| key           | 执行时实际用到的索引名称                                     |
| key_len       | 执行时用到的索引长度                                         |
| ref           | 哪些表列或常数列与“key”列出的索引名进行了比较操作            |
| rows          | 执行的语句所涉及的记录数，INNODB引擎为估值                   |
| filtered      | 返回结果的行记录数占执行中所有读取到的行记录数的百分比       |
| Extra         | 执行SQL语句时一些相关的补充信息                              |



1. 不要使用表达式作为查询条件

    当使用表达式时，就不会使用缓存，因为这些函数的返回是不确定的

    方式一：`select * from stu where id+1 < 5; # 不推荐`

    方式二：`select * from stu where id < 5-1; # 推荐`

2. 尽量使用 in 来替代 or

3. 有条件使用where 就不使用having

4. 使用like操作符时通配符要放在右侧

    方式一：`select * from stu where name like '_号_'; # 不推荐`

    方式二：`select * from stu where name like 'a号_';  # 推荐`





### 优化查询

1. 如果数据库表需要事务处理，应考虑InnoDB，因其完全符合ACID特性；如果不需要事务处理，使用默认存储引擎MyISAM比较明智；
2. 分表分库，主从；
3. 对查询进行优化，要尽量避免全表扫描，首先应考虑在where 及 order by 涉及的列上建立索引；
3. 应尽量避免在where 子句中对字段进行null 值判断、 !=  或 <>  操作符，否则将导致引擎放弃使用索引而进行全表扫描；
3. 应尽量避免在where 子句中使用or 来连接条件，如果一个字段有索引，将导致引擎放弃使用索引而进行全表扫描；
3. update ，如果只修改1,2个字段，不要update全部字段，否则频繁调用会引起明显的性能消耗，同时带来大量日志；
3. 对于多张大数据量（几百条算大）的表join，要先分页再join；





```mysql
select avg(单价) a from 商品表 group by 类别 having a<100;

select deptno,count(*), avg(sal) avgSal 
from emp 
group by deptno having avgSal>2000
order by avgSal desc;

select avg(price) 
from 商品表
group by 商品种类 having 商品种类 in (238,917);

# 5.
select deptno, sum(sal), avg(sal) avgSal
from emp
where sal between 1000 and 3000
group by deptno having avg>=2000;
order by avgSal;

# 6. 
select 年 count(*)
from emp
group by 年份;

# 7. 
select deptno, avg(sql) as a
from emp
group by deptno having max(a);


#-------------
select *from emp where sal = (
    select max(sal) from emp;
);

# 3.
select *from emp where sal > (
    select max(sal) from emp where detp = 20;
)

# 4.
select * from emp where job = (
    select job from emp where 员工名 = 'jones';
)

# 5. 
select * from emp where deptno in (
    select deptno from emp where empno = (
        select min(sal) from emp
    );
)

# 6. 
select * from emp where 入职时间 = (
    select max(入职时间) from emp;
)

select * from dept where deptno = (
    select deptno from emp where 员工名= king ;
)

# 8.
select * from dept where deptno in (
    select deptno from emp;
)


```
