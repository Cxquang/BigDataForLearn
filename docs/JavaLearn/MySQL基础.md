# 一、数据库介绍
## 1.1 为什么要学习数据库
* 持久化数据到本地
* 可以实现结构化查询，方便管理

## 1.2数据库的相关概念
* DB：数据库，保存一组有组织的数据的容器
* DBMS：数据库管理系统，又称为数据库软件（产品），用于管理DB中的数据
* SQL:结构化查询语言，用于和DBMS通信的语言

## 1.3数据库存储数据的特点
* 将数据放到表中，表再放到库中
* 一个数据库中可以有多个表，每个表都有一个的名字，用来标识自己。表名具有唯一性。
* 表具有一些特性，这些特性定义了数据在表中如何存储，类似java中 “类”的设计。
* 表由列组成，我们也称为字段。所有表都是由一个或多个列组成的，每一列类似java 中的”属性”
* 表中的数据是按行存储的，每一行类似于java中的“对象”。

# 二、初始MySQL
## 2.1 MySQL产品的介绍        
## 2.2 MySQL产品的安装          ★        
## 2.3 MySQL服务的启动和停止     ★
* 方式一：计算机——右击管理——服务
* 方式二：通过管理员身份运行
* net start 服务名（启动服务）
* net stop 服务名（停止服务）

## 2.4 MySQL服务的登录和退出     ★   
* 方式一：通过mysql自带的客户端<br>
	只限于root用户

* 方式二：通过windows自带的客户端<br>
	登录：<br>
	mysql 【-h主机名 -P端口号 】-u用户名 -p密码<br>
	
	退出：<br>
	exit或ctrl+C<br>

## 2.5 MySQL的常见命令和语法规范   
### 2.5.1 MySQL的常见命令 
* 查看当前所有的数据库：show databases;
* 打开指定的库：use 库名；
* 查看当前库的所有表：show tables;
* 查看其它库的所有表：show tables from 库名;
* 创建表

```sql
create table 表名(
	
	列名 列类型,
	列名 列类型，
	。。。
);
```

* 查看表结构：desc 表名;
* 查看服务器的版本<br>
	方式一：登录到mysql服务端<br>
	select version();<br>
	方式二：没有登录到mysql服务端<br>
	mysql --version或mysql --V<br>

### 2.5.2 MySQL的语法规范
* **<font color=red size=4>不区分大小写,但建议关键字大写，表名、列名小写</font>**
* 每条命令最好用分号结尾【也可以\g结尾】
* 每条命令根据需要，可以进行缩进 或换行
* 注释<br>
单行注释：#注释文字<br>
单行注释：-- 注释文字<br>
多行注释：/* 注释文字  */<br>
	
### 2.5.3 SQL的语言分类
* DQL（Data Query Language）：数据查询语言【select】
* DML(Data Manipulate Language):数据操作语言【insert 、update、delete】
* DDL（Data Define Languge）：数据定义语言【create、drop、alter】
* TCL（Transaction Control Language）：事务控制语言【commit、rollback】

### 2.6 导入数据库
为了方便学习，这里准备两份SQL文件，通过可视化数据库管理工具导入即可<br>

* [girls.sql](https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/girls.sql ':include')
* [myemployees.sql](https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/myemployees.sql ':include')<br>

**<font color=black size=4>在图形界面中，选中连接对象，右键执行SQL脚本</font>**

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/1、执行SQL脚本.png"/> </div>
<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/1、执行SQL脚本1.png"/> </div>
<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/1、执行SQL脚本2.png"/> </div>

### 2.7 myemployees库表格介绍
* employees表

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/2、employees表.png"/> </div>

* departments表

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/2、departments表.png"/> </div>

* jobs表

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/2、jobs表.png"/> </div>

* locations表

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/2、locations表.png"/> </div>

* job_grades表：工资级别表，手动创建

```sql
CREATE TABLE job_grades
(grade_level VARCHAR(3),
 lowest_sal  int,
 highest_sal int);

INSERT INTO job_grades
VALUES ('A', 1000, 2999);

INSERT INTO job_grades
VALUES ('B', 3000, 5999);

INSERT INTO job_grades
VALUES('C', 6000, 9999);

INSERT INTO job_grades
VALUES('D', 10000, 14999);

INSERT INTO job_grades
VALUES('E', 15000, 24999);

INSERT INTO job_grades
VALUES('F', 25000, 40000);
```


### 2.8 girls库表格介绍
* admin表

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/7、admin表.png"/> </div>

* beauty表

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/5、beauty表.png"/> </div>

* boys表

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/6、boys表.png"/> </div>

# 三、DQL语言的学习   ★              
## 3.1 基础查询        ★
### 3.1.1 语法
* SELECT  查询列表 【FROM 表名】;

* 类似于Java中 :System.out.println(要打印的东西);
* 特点：<br>
①通过select查询完的结果 ，是一个虚拟的表格，不是真实存在<br>
② 要查询的东西 可以是常量值、可以是表达式、可以是字段、可以是函数

### 3.1.2 示例
#### 3.1.2.1 查询字段
select 字段名 from 表名;

```sql
【limit是截取查询的条数】
mysql> SELECT last_name FROM employees LIMIT 5;
+-----------+
| last_name |
+-----------+
| K_ing     |
| Kochhar   |
| De Haan   |
| Hunold    |
| Ernst     |
+-----------+
10 rows in set (0.00 sec)
```

* 查询多个字段：select 字段名，字段名 from 表名;
* 查询所有字段：select * from 表名
#### 3.1.2.2  查询常量
select 常量值;【注意：字符型和日期型的常量值必须用单引号引起来，数值型不需要】

```sql
mysql> SELECT 100;
+-----+
| 100 |
+-----+
| 100 |
+-----+
1 row in set (0.00 sec)
----------------------------
mysql> SELECT 'john';
+------+
| john |
+------+
| john |
+------+
1 row in set (0.00 sec)
```

#### 3.1.2.3 查询函数
select 函数名(实参列表);

```sql
mysql> SELECT VERSION();
+-----------+
| VERSION() |
+-----------+
| 5.5.15    |
+-----------+
1 row in set (0.00 sec)
```
#### 3.1.2.4 查询表达式
select 100/1234;
#### 3.1.2.5 起别名
①as；②空格

```sql
mysql> SELECT 100%98 AS '结果';
+------+
| 结果     |
+------+
|    2 |
+------+
1 row in set (0.00 sec)
```

#### 3.1.2.6 去重
select distinct 字段名 from 表名;

```sql
mysql> SELECT DISTINCT department_id FROM employees;
+---------------+
| department_id |
+---------------+
|          NULL |
|            10 |
|            20 |
|            30 |
|            40 |
|            50 |
|            60 |
|            70 |
|            80 |
|            90 |
|           100 |
|           110 |
+---------------+
12 rows in set (0.00 sec)
```

#### 3.1.2.7 +运算符
作用：做加法运算<br>
select 数值+数值; 直接运算<br>
select 字符+数值;先试图将字符转换成数值，如果转换成功，则继续运算；否则转换成0，再做运算<br>
select null+值;结果都为null<br>

```sql
mysql> SELECT 100+90;
+--------+
| 100+90 |
+--------+
|    190 |
+--------+
1 row in set (0.00 sec)

mysql> SELECT 'john'+90;
+-----------+
| 'john'+90 |
+-----------+
|        90 |
+-----------+
1 row in set, 1 warning (0.00 sec)
```

java中的+号：<br>
①运算符，两个操作符都为数值型<br>
②连接符，只要有一个操作数为字符串

#### 3.1.2.8【补充】concat函数
功能：拼接字符<br>
select concat(字符1，字符2，字符3,...);

```sql
mysql> SELECT CONCAT(last_name,first_name) AS '姓名' FROM employees LIMIT 5;
+-----------------+
| 姓名                |
+-----------------+
| K_ingSteven     |
| KochharNeena    |
| De HaanLex      |
| HunoldAlexander |
| ErnstBruce      |
+-----------------+
5 rows in set (0.00 sec)
```

#### 3.1.2.9【补充】ifnull函数
功能：判断某字段或表达式是否为null，如果为null 返回指定的值，否则返回原本的值<br>
select ifnull(commission_pct,0) from employees;

#### 3.1.2.10【补充】isnull函数
功能：判断某字段或表达式是否为null，如果是，则返回1，否则返回0<br>

## 3.2 条件查询  	   ★
### 3.2.1 语法
select 查询列表  from 表名  where 筛选条件
### 3.2.2 筛选条件的分类
#### 3.2.2.1 简单条件运算符
* `> < = <> != >= <=  <=>安全等于`
* \!=和<>都是不等于，但mysql中还是推荐使用<>

#### 3.2.2.2 逻辑运算符
* 作用：用于连接条件表达式<br>

&& || !<br>
and or not<br>

* && 和 and ：两个条件都为true，结果为true，反之为false

```sql
【查询工资在10000到20000之间的员工名、工资以及奖金】
mysql> SELECT
    -> last_name,
    -> salary,
    -> commission_pct
    -> FROM
    -> employees
    -> WHERE
    -> salary>=10000 AND salary<=20000
    -> LIMIT 5;
+-----------+----------+----------------+
| last_name | salary   | commission_pct |
+-----------+----------+----------------+
| Kochhar   | 17000.00 |           NULL |
| De Haan   | 17000.00 |           NULL |
| Greenberg | 12000.00 |           NULL |
| Raphaely  | 11000.00 |           NULL |
| Russell   | 14000.00 |           0.40 |
+-----------+----------+----------------+
5 rows in set (0.00 sec)
```

* || or：只要有一个条件为true，结果为true，反之为false
* !  not：如果连接的条件本身为false，结果为true，反之为false

```sql
【查询部门编号不是在90到110之间，或者工资高于15000的员工信息】
mysql> SELECT
    -> *
    -> FROM
    -> employees
    -> WHERE
    -> NOT(department_id>=90 AND  department_id<=110) OR salary>15000
    -> LIMIT 5;
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```

#### 3.2.2.3 模糊查询
* like:一般搭配通配符使用，可以判断字符型或数值型
通配符：%任意多个字符【包含0个字符】，_任意单个字符

```sql
mysql> select
    -> *
    -> from
    -> employees
    -> where
    -> last_name like '%a%'
    -> limit 5;
+-------------+------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id     | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP      | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP      | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         105 | David      | Austin    | DAUSTIN  | 590.423.4569 | IT_PROG    |  4800.00 |           NULL |        103 |            60 | 1998-03-03 00:00:00 |
|         106 | Valli      | Pataballa | VPATABAL | 590.423.4560 | IT_PROG    |  4800.00 |           NULL |        103 |            60 | 1998-03-03 00:00:00 |
|         109 | Daniel     | Faviet    | DFAVIET  | 515.124.4169 | FI_ACCOUNT |  9000.00 |           NULL |        108 |           100 | 1998-03-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)

【查询员工名中第三个字符为e，第五个字符为a的员工名和工资】
mysql> select
    -> last_name,
    -> salary
    -> FROM
    -> employees
    -> WHERE
    -> last_name LIKE '__n_l%'
    -> limit 5;
+-----------+---------+
| last_name | salary  |
+-----------+---------+
| Hunold    | 9000.00 |
+-----------+---------+
1 row in set (0.00 sec)

【查询员工名中第二个字符为_的员工名】
mysql> SELECT
    -> last_name
    -> FROM
    -> employees
    -> WHERE
    -> last_name LIKE '_\_%';
+-----------+
| last_name |
+-----------+
| K_ing     |
| K_ing     |
+-----------+
2 rows in set (0.00 sec)
--------------------------------------------
mysql> SELECT
    -> last_name
    -> FROM
    -> employees
    -> WHERE
    -> last_name LIKE '_$_%' ESCAPE '$'; --说明$为转移字符
+-----------+
| last_name |
+-----------+
| K_ing     |
| K_ing     |
+-----------+
2 rows in set (0.00 sec)
```

* between and<br>
①使用between and 可以提高语句的简洁度<br>
②包含临界值<br>
③两个临界值不要调换顺序

```sql
【查询员工编号在100到120之间的员工信息】
mysql> SELECT
    -> *
    -> FROM
    -> employees
    -> WHERE
    -> employee_id BETWEEN 100 AND 120
    -> limit 5;
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```

* in ：判断某字段的值是否属于in列表中的某一项<br>
特点：<br>
①使用in提高语句简洁度<br>
②in列表的值类型必须一致或兼容<br>
③in列表中不支持通配符

```sql
【查询员工的工种编号是 IT_PROG、AD_VP、AD_PRES中的一个员工名和工种编号】
mysql> SELECT
    -> last_name,
    -> job_id
    -> FROM
    -> employees
    -> WHERE
    -> job_id IN( 'IT_PROT' ,'AD_VP','AD_PRES');
+-----------+---------+
| last_name | job_id  |
+-----------+---------+
| K_ing     | AD_PRES |
| Kochhar   | AD_VP   |
| De Haan   | AD_VP   |
+-----------+---------+
3 rows in set (0.00 sec)
------------------------------------------------
mysql> SELECT
    -> last_name,
    -> job_id
    -> FROM
    -> employees
    -> WHERE
    -> job_id = 'IT_PROT' OR job_id = 'AD_VP' OR JOB_ID ='AD_PRES';
+-----------+---------+
| last_name | job_id  |
+-----------+---------+
| K_ing     | AD_PRES |
| Kochhar   | AD_VP   |
| De Haan   | AD_VP   |
+-----------+---------+
3 rows in set (0.00 sec)
```

* is null /is not null：用于判断null值<br>
=或<>不能用于判断null值<br>
is null或is not null 可以判断null值<br>

**<font color=red size=4>is null  和  <=>的比较</font>**<br>

<table>
<thead>
<tr>
<th></th>
<th>普通类型的数值</th>
<th>null值</th>
<th>可读性</th>
</tr>
</thead>
<tbody>
<tr>
<th>is null</th>
<th>×</th>
<th>√ </th>
<th>√ </th>
</tr>
<tr>
<th><=></th>
<th>√ </th>
<th>√ </th>
<th>×</th>
</tr>
</tbody>
</table>

```sql
【查询没有奖金的员工名和奖金率】
mysql> SELECT
    -> last_name,
    -> commission_pct
    -> FROM
    -> employees
    -> WHERE
    -> commission_pct IS NULL limit 5;
+-----------+----------------+
| last_name | commission_pct |
+-----------+----------------+
| K_ing     |           NULL |
| Kochhar   |           NULL |
| De Haan   |           NULL |
| Hunold    |           NULL |
| Ernst     |           NULL |
+-----------+----------------+
5 rows in set (0.00 sec)
-------------------------------------------
mysql> SELECT
    -> last_name,
    -> commission_pct
    -> FROM
    -> employees
    -> WHERE
    -> commission_pct <=>NULL limit 5;
+-----------+----------------+
| last_name | commission_pct |
+-----------+----------------+
| K_ing     |           NULL |
| Kochhar   |           NULL |
| De Haan   |           NULL |
| Hunold    |           NULL |
| Ernst     |           NULL |
+-----------+----------------+
5 rows in set (0.00 sec)
【查询工资为12000的员工信息】
mysql> SELECT
    -> last_name,
    -> salary
    -> FROM
    -> employees
    ->
    -> WHERE
    -> salary <=> 12000;
+-----------+----------+
| last_name | salary   |
+-----------+----------+
| Greenberg | 12000.00 |
| Errazuriz | 12000.00 |
| Higgins   | 12000.00 |
+-----------+----------+
3 rows in set (0.00 sec)
```

## 3.3 排序查询  	   ★
### 3.3.1 语法
select 查询列表<br>
from 表名<br>
【where  筛选条件】<br>
order by 排序的字段或表达式 asc|desc;<br>

* 特点：<br>
1、asc代表的是升序，可以省略；desc代表的是降序<br>
2、order by子句可以支持 单个字段、别名、表达式、函数、多个字段<br>
3、order by子句在查询语句的最后面，除了limit子句<br>

### 3.3.2 示例
#### 3.3.2.1 按单个字段排序
```sql
mysql> SELECT * FROM employees ORDER BY salary DESC limit 5;
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number       | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567       | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568       | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569       | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         145 | John       | Russell   | JRUSSEL  | 011.44.1344.429268 | SA_MAN  | 14000.00 |           0.40 |        100 |            80 | 2002-12-23 00:00:00 |
|         146 | Karen      | Partners  | KPARTNER | 011.44.1344.467268 | SA_MAN  | 13500.00 |           0.30 |        100 |            80 | 2002-12-23 00:00:00 |
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```

#### 3.3.2.2 添加筛选条件再排序

```sql
【查询部门编号>=90的员工信息，并按员工编号降序】
mysql> SELECT *
    -> FROM employees
    -> WHERE department_id>=90
    -> ORDER BY employee_id DESC limit 5;
+-------------+-------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name  | last_name | email    | phone_number | job_id     | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+-------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
|         206 | William     | Gietz     | WGIETZ   | 515.123.8181 | AC_ACCOUNT |  8300.00 |           NULL |        205 |           110 | 2016-03-03 00:00:00 |
|         205 | Shelley     | Higgins   | SHIGGINS | 515.123.8080 | AC_MGR     | 12000.00 |           NULL |        101 |           110 | 2016-03-03 00:00:00 |
|         113 | Luis        | Popp      | LPOPP    | 515.124.4567 | FI_ACCOUNT |  6900.00 |           NULL |        108 |           100 | 2000-09-09 00:00:00 |
|         112 | Jose Manuel | Urman     | JMURMAN  | 515.124.4469 | FI_ACCOUNT |  7800.00 |           NULL |        108 |           100 | 2000-09-09 00:00:00 |
|         111 | Ismael      | Sciarra   | ISCIARRA | 515.124.4369 | FI_ACCOUNT |  7700.00 |           NULL |        108 |           100 | 2000-09-09 00:00:00 |
+-------------+-------------+-----------+----------+--------------+------------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```

#### 3.3.2.3 按表达式排序

```sql
【查询员工信息 按年薪升序】
mysql> SELECT *,salary*12*(1+IFNULL(commission_pct,0)) '年薪'
    -> FROM employees
    -> ORDER BY '年薪' ASC limit 5;
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+-----------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            | 年薪         |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+-----------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 | 288000.00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 | 204000.00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 | 204000.00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 | 108000.00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |  72000.00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+-----------+
5 rows in set (0.00 sec)
```

#### 3.3.2.4 按函数排序

```sql
【查询员工名，并且按名字的长度降序】
mysql> SELECT LENGTH(last_name),last_name
    -> FROM employees
    -> ORDER BY LENGTH(last_name) DESC limit 5;
+-------------------+-------------+
| LENGTH(last_name) | last_name   |
+-------------------+-------------+
|                11 | Mikkilineni |
|                10 | Philtanker  |
|                10 | Colmenares  |
|                10 | Livingston  |
|                 9 | Dellinger   |
+-------------------+-------------+
5 rows in set (0.00 sec)
```

#### 3.3.2.5 按多个字段排序

```sql
【查询员工信息，要求先按工资降序，再按employee_id升序】
mysql> SELECT *
    -> FROM employees
    -> ORDER BY salary DESC,employee_id ASC limit 5;
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number       | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567       | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568       | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569       | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         145 | John       | Russell   | JRUSSEL  | 011.44.1344.429268 | SA_MAN  | 14000.00 |           0.40 |        100 |            80 | 2002-12-23 00:00:00 |
|         146 | Karen      | Partners  | KPARTNER | 011.44.1344.467268 | SA_MAN  | 13500.00 |           0.30 |        100 |            80 | 2002-12-23 00:00:00 |
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```

## 3.4 常见函数        ★
* 概念：类似于java的方法，将一组逻辑语句封装在方法体中，对外暴露方法名
* 好处：1、隐藏了实现细节  2、提高代码的重用性
* 调用：select 函数名(实参列表) 【from 表】;
* 特点：<br>
①叫什么（函数名）<br>
②干什么（函数功能）

* 分类：<br>
1、单行函数<br>
如 concat、length、ifnull等<br>
2、分组函数<br>
功能：做统计使用，又称为统计函数、聚合函数、组函数<br>
	
## 3.5 单行函数
### 3.5.1 字符函数
#### 3.5.1.1 length
* 获取字节个数(utf-8一个汉字代表3个字节,gbk为2个字节)
* show variables like'%char%';
* SELECT LENGTH('john');
* SELECT LENGTH('蔡贤权hahaha'); --15个字节

#### 3.5.1.2 concat
* 拼接字符串
* SELECT CONCAT(last_name,'_',first_name) 姓名 FROM employees;

#### 3.5.1.3 substr
* 也可以写成substring
* 索引从1开始

```sql
【截取从指定索引处后面所有字符】
mysql> SELECT SUBSTR('李莫愁爱上了陆展元',7)  out_put;
+---------+
| out_put |
+---------+
| 陆展元     |
+---------+
1 row in set (0.00 sec)
【截取从指定索引处指定字符长度的字符】
mysql> SELECT SUBSTR('李莫愁爱上了陆展元',1,3) out_put;
+---------+
| out_put |
+---------+
| 李莫愁       |
+---------+
1 row in set (0.00 sec)
【姓名中首字符大写，其他字符小写然后用_拼接，显示出来】
mysql> SELECT CONCAT(UPPER(SUBSTR(last_name,1,1)),'_',LOWER(SUBSTR(last_name,2)))  out_put
    -> FROM employees limit 5;
+----------+
| out_put  |
+----------+
| K__ing   |
| K_ochhar |
| D_e haan |
| H_unold  |
| E_rnst   |
+----------+
5 rows in set (0.00 sec)
```

#### 3.5.1.4 instr
返回子串第一次出现的索引，如果找不到返回0
```sql
mysql> SELECT INSTR('杨不殷六侠悔爱上了殷六侠','殷八侠') AS out_put;
+---------+
| out_put |
+---------+
|       0 |
+---------+
1 row in set (0.00 sec)
mysql> SELECT INSTR('杨不殷六侠悔爱上了殷六侠','殷六侠') AS out_put;
+---------+
| out_put |
+---------+
|       3 |
+---------+
1 row in set (0.00 sec)
```

#### 3.5.1.5 trim
去掉前后空白符
```sql
mysql>  SELECT LENGTH(TRIM('    张翠山    ')) AS out_put;
+---------+
| out_put |
+---------+
|       9 |
+---------+
1 row in set (0.00 sec)
-------------------------------------------
mysql> SELECT TRIM('a' FROM 'aaaaaaaaa张aaaaaaaaaaaa翠山aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa')  AS out_put;
+--------------------+
| out_put            |
+--------------------+
| 张aaaaaaaaaaaa翠山      |
+--------------------+
1 row in set (0.00 sec)
```

#### 3.5.1.6 upper&lower
* SELECT UPPER('john'); --JOHN
* SELECT LOWER('joHn'); --john

```sql
【将姓变大写，名变小写，然后拼接】
mysql> SELECT CONCAT(UPPER(last_name),LOWER(first_name))  '姓名' FROM employees limit 5;
+-----------------+
| 姓名                |
+-----------------+
| K_INGsteven     |
| KOCHHARneena    |
| DE HAANlex      |
| HUNOLDalexander |
| ERNSTbruce      |
+-----------------+
5 rows in set (0.00 sec)
```

#### 3.5.1.7 lpad&rpad
用指定的字符实现左填充【右填充】指定长度
```sql
mysql> SELECT LPAD('殷素素',10,'*') AS out_put;
+------------+
| out_put    |
+------------+
| *******殷素素       |
+------------+
1 row in set (0.00 sec)
【如果指定长度小于原字符串，那么将是截取】
mysql> SELECT LPAD('殷素素',2,'*') AS out_put;
+---------+
| out_put |
+---------+
| 殷素        |
+---------+
1 row in set (0.00 sec)
```
#### 3.5.1.8 replace
```sql
mysql> SELECT REPLACE('周芷若周芷若周芷若周芷若张无忌爱上了周芷若','周芷若','赵敏') AS out_put;
+----------------------------------+
| out_put                          |
+----------------------------------+
| 赵敏赵敏赵敏赵敏张无忌爱上了赵敏                               |
+----------------------------------+
1 row in set (0.00 sec)
```

### 3.5.2 数学函数
#### 3.5.2.1  round
* 四舍五入
* SELECT ROUND(-1.55); --   -2
* SELECT ROUND(1.567,2); --1.57

#### 3.5.2.2 ceil
* 向上取整,返回>=该参数的最小整数
* SELECT CEIL(-1.02); -- -1.0
* SELECT CEIL(1.02); -- 2.0

#### 3.5.2.3 floor
* 向下取整，返回<=该参数的最大整数
* SELECT FLOOR(-9.99); -- -9
* SELECT FLOOR(9.99); -- 9

#### 3.5.2.4 truncate
* 截断
* SELECT TRUNCATE(1.69999,1);  --1.6【保留小数点后一位】

#### 3.5.2.5 mod
* 取余【被除数为正结果为正，被除数为负结果为负，公式a-a/b*b】
* SELECT MOD(10,-3); -- 1
* SELECT MOD(-10,-3); -- -1

### 3.5.3 日期函数
#### 3.5.3.1 now
* 返回当前系统日期+时间
* SELECT NOW(); --2019-08-21 15:38:02

#### 3.5.3.2 curdate
* 返回当前系统日期，不包含时间
* SELECT CURDATE();--2019-08-21 

#### 3.5.3.3 curtime
* 返回当前时间，不包含日期
* SELECT CURTIME(); --15:38:02

#### 3.5.3.4 year
* SELECT YEAR(NOW()) 年;
* SELECT YEAR('1998-1-1') 年;

#### 3.5.3.5 month
* ELECT MONTH(NOW()) 月; --8月

#### 3.5.3.6 monthname
* SELECT MONTHNAME(NOW()) 月;--August 月

#### 3.5.3.7 day&hour&minute&second
#### 3.5.3.8 str_to_date
* 将字符通过指定的格式转换成日期

```sql
mysql> SELECT STR_TO_DATE('1998-3-2','%Y-%c-%d') AS out_put;
+------------+
| out_put    |
+------------+
| 1998-03-02 |
+------------+
1 row in set (0.00 sec)
---------------------------------------------------------------
【查询入职日期为1992-4-3的员工信息】
mysql> SELECT * FROM employees WHERE hiredate = '1992-4-3';
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
【通过对字符串日期进行格式转换再查找】
mysql> SELECT * FROM employees WHERE hiredate = STR_TO_DATE('4-3 1992','%c-%d %Y');
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```


<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/3、日期格式表.png"/> </div>

#### 3.5.3.9 date_format
将日期转换成字符
```sql
mysql> SELECT DATE_FORMAT(NOW(),'%y年%m月%d日') AS out_put;
+--------------+
| out_put      |
+--------------+
| 19年08月21日       |
+--------------+
1 row in set (0.00 sec)
【查询有奖金的员工名和入职日期(xx月/xx日 xx年)】
mysql> SELECT last_name,DATE_FORMAT(hiredate,'%m月/%d日 %y年') '入职日期'
    -> FROM employees
    -> WHERE commission_pct IS NOT NULL LIMIT 5;
+-----------+----------------+
| last_name | 入职日期              |
+-----------+----------------+
| Russell   | 12月/23日 02年       |
| Partners  | 12月/23日 02年       |
| Errazuriz | 12月/23日 02年       |
| Cambrault | 12月/23日 02年       |
| Zlotkey   | 12月/23日 02年       |
+-----------+----------------+
5 rows in set (0.00 sec)
```

### 3.5.4 其他函数
#### 3.5.4.1 version
```sql
【查看当前mysql数据库版本】
mysql> SELECT VERSION();
+-----------+
| VERSION() |
+-----------+
| 5.5.15    |
+-----------+
1 row in set (0.00 sec)
```

#### 3.5.4.2 database
```sql
【查看当前数据库】
mysql> SELECT DATABASE();
+-------------+
| DATABASE()  |
+-------------+
| myemployees |
+-------------+
1 row in set (0.00 sec)
```

#### 3.5.4.3 user
```sql
【查看当前用户】
mysql> SELECT USER();
+----------------+
| USER()         |
+----------------+
| root@localhost |
+----------------+
1 row in set (0.00 sec)
```

### 3.5.5 控制函数
#### 3.5.5.1 if
* if...else... 的效果

```sql
mysql> SELECT IF(10<5,'大','小');
+--------------------+
| IF(10<5,'大','小')    |
+--------------------+
| 小                  |
+--------------------+
1 row in set (0.00 sec)
----------------------------------------
mysql> SELECT last_name,commission_pct,IF(commission_pct IS NULL,'没奖金，呵呵','有奖金，嘻嘻') '备注'
    -> FROM employees limit 5;
+-----------+----------------+--------------+
| last_name | commission_pct | 备注            |
+-----------+----------------+--------------+
| K_ing     |           NULL | 没奖金，呵呵           |
| Kochhar   |           NULL | 没奖金，呵呵           |
| De Haan   |           NULL | 没奖金，呵呵           |
| Hunold    |           NULL | 没奖金，呵呵           |
| Ernst     |           NULL | 没奖金，呵呵           |
+-----------+----------------+--------------+
5 rows in set (0.00 sec)
```

#### 3.5.5.2 case
* 使用一： switch case 的效果

```sql
/*
java中
switch(变量或表达式){
	case 常量1：语句1;break;
	...
	default:语句n;break;


}

mysql中

case 要判断的字段或表达式
when 常量1 then 要显示的值1或语句1;
when 常量2 then 要显示的值2或语句2;
...
else 要显示的值n或语句n;
end
*/

/*案例：查询员工的工资，要求

部门号=30，显示的工资为1.1倍
部门号=40，显示的工资为1.2倍
部门号=50，显示的工资为1.3倍
其他部门，显示的工资为原工资
*/
mysql> SELECT salary '原始工资',department_id,
    -> CASE department_id
    -> WHEN 30 THEN salary*1.1
    -> WHEN 40 THEN salary*1.2
    -> WHEN 50 THEN salary*1.3
    -> ELSE salary
    -> END AS '新工资'
    -> FROM employees order by department_id asc limit 5;
+----------+---------------+----------+
| 原始工资       | department_id | 新工资        |
+----------+---------------+----------+
|  7000.00 |          NULL |  7000.00 |
|  4400.00 |            10 |  4400.00 |
|  6000.00 |            20 |  6000.00 |
| 13000.00 |            20 | 13000.00 |
|  2500.00 |            30 |  2750.00 |
+----------+---------------+----------+
5 rows in set (0.00 sec)
```

* 使用二：类似于 多重if

```sql
/*
java中：
if(条件1){
	语句1；
}else if(条件2){
	语句2；
}
...
else{
	语句n;
}

mysql中：

case 
when 条件1 then 要显示的值1或语句1
when 条件2 then 要显示的值2或语句2
。。。
else 要显示的值n或语句n
end

案例：查询员工的工资的情况
如果工资>20000,显示A级别
如果工资>15000,显示B级别
如果工资>10000，显示C级别
否则，显示D级别
*/
mysql> SELECT salary,
    -> CASE
    -> WHEN salary>20000 THEN 'A'
    -> WHEN salary>15000 THEN 'B'
    -> WHEN salary>10000 THEN 'C'
    -> ELSE 'D'
    -> END AS '工资级别'
    -> FROM employees limit 5;
+----------+----------+
| salary   | 工资级别        |
+----------+----------+
| 24000.00 | A        |
| 17000.00 | B        |
| 17000.00 | B        |
|  9000.00 | D        |
|  6000.00 | D        |
+----------+----------+
5 rows in set (0.00 sec)
```

## 3.6 分组函数        ★
### 3.6.1 介绍
* 用作统计使用，又称为聚合函数或统计函数或组函数
* 分类：sum 求和、avg 平均值、max 最大值 、min 最小值 、count 计算个数
* 特点：<br>
1、sum、avg一般用于处理数值型；max、min、count可以处理任何类型<br>
2、以上分组函数都忽略null值<br>
3、可以和distinct搭配实现去重的运算<br>
4、count函数的单独介绍<br>
一般使用count(*)用作统计行数<br>
5、和分组函数一同查询的字段要求是group by后的字段<br>

### 3.6.2 sum求和

```sql
mysql> SELECT SUM(salary) FROM employees;
+-------------+
| SUM(salary) |
+-------------+
|   691400.00 |
+-------------+
1 row in set (0.00 sec)
```
### 3.6.3 avg 平均值

```sql
mysql> SELECT AVG(salary) FROM employees;
+-------------+
| AVG(salary) |
+-------------+
| 6461.682243 |
+-------------+
1 row in set (0.00 sec)
```

### 3.6.4 max最大值&max最小值

```sql
mysql> SELECT MAX(salary) FROM employees;
+-------------+
| MAX(salary) |
+-------------+
|    24000.00 |
+-------------+
1 row in set (0.00 sec)
mysql> SELECT MIN(salary) FROM employees;
+-------------+
| MIN(salary) |
+-------------+
|     2100.00 |
+-------------+
1 row in set (0.00 sec)
```

### 3.6.5 count计算个数

```sql
mysql> SELECT COUNT(salary) FROM employees;
+---------------+
| COUNT(salary) |
+---------------+
|           107 |
+---------------+
1 row in set (0.00 sec)
```

## 3.7 分组查询		   ★
### 3.7.1 介绍&语法
select 查询列表<br>
from 表<br>
【where 筛选条件】<br>
group by 分组的字段<br>
【order by 排序的字段】;<br>

```sql
【引入：查询每个部门的平均工资】
mysql> SELECT department_id, AVG(salary) FROM employees group by department_id;
+---------------+--------------+
| department_id | AVG(salary)  |
+---------------+--------------+
|          NULL |  7000.000000 |
|            10 |  4400.000000 |
|            20 |  9500.000000 |
|            30 |  4150.000000 |
|            40 |  6500.000000 |
|            50 |  3475.555556 |
|            60 |  5760.000000 |
|            70 | 10000.000000 |
|            80 |  8955.882353 |
|            90 | 19333.333333 |
|           100 |  8600.000000 |
|           110 | 10150.000000 |
+---------------+--------------+
12 rows in set (0.00 sec)
```

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/4、分组查询.png"/> </div>

* 特点：<br>
1、和分组函数一同查询的字段必须是group by后出现的字段<br>
2、筛选分为两类：分组前筛选和分组后筛选<br>

<table>
<thead>
<tr>
<th></th>
<th>针对的表</th>
<th>位置</th>
<th>连接的关键字</th>
</tr>
</thead>
<tbody>
<tr>
<th>分组前筛选</th>
<th>原始表</th>
<th>group by前 </th>
<th>where </th>
</tr>
<tr>
<th>分组后筛选</th>
<th>group by后的结果集 </th>
<th>group by后 </th>
<th>having</th>
</tr>
</tbody>
</table>

问题1：分组函数做筛选能不能放在where后面<br>
答：不能<br>

问题2：where——group by——having<br>

一般来讲，能用分组前筛选的，尽量使用分组前筛选，提高效率<br>

3、分组可以按单个字段也可以按多个字段<br>
4、可以搭配着排序使用<br>

### 3.7.2 简单的分组

```sql
【查询每个工种的员工平均工资】
mysql> SELECT AVG(salary),job_id
    -> FROM employees
    -> GROUP BY job_id;
+--------------+------------+
| AVG(salary)  | job_id     |
+--------------+------------+
|  8300.000000 | AC_ACCOUNT |
| 12000.000000 | AC_MGR     |
|  4400.000000 | AD_ASST    |
| 24000.000000 | AD_PRES    |
| 17000.000000 | AD_VP      |
|  7920.000000 | FI_ACCOUNT |
| 12000.000000 | FI_MGR     |
|  6500.000000 | HR_REP     |
|  5760.000000 | IT_PROG    |
| 13000.000000 | MK_MAN     |
|  6000.000000 | MK_REP     |
| 10000.000000 | PR_REP     |
|  2780.000000 | PU_CLERK   |
| 11000.000000 | PU_MAN     |
| 12200.000000 | SA_MAN     |
|  8350.000000 | SA_REP     |
|  3215.000000 | SH_CLERK   |
|  2785.000000 | ST_CLERK   |
|  7280.000000 | ST_MAN     |
+--------------+------------+
19 rows in set (0.00 sec)

【查询每个位置的部门个数】
mysql> SELECT COUNT(*),location_id
    -> FROM departments
    -> GROUP BY location_id;
+----------+-------------+
| COUNT(*) | location_id |
+----------+-------------+
|        1 |        1400 |
|        1 |        1500 |
|       21 |        1700 |
|        1 |        1800 |
|        1 |        2400 |
|        1 |        2500 |
|        1 |        2700 |
+----------+-------------+
7 rows in set (0.00 sec)
```
### 3.7.3 添加分组前筛选

```sql
【查询邮箱中包含a字符的 每个部门的最高工资】
mysql>  SELECT MAX(salary),department_id FROM employees WHERE email LIKE '%a%' GROUP BY department_id;
+-------------+---------------+
| MAX(salary) | department_id |
+-------------+---------------+
|     7000.00 |          NULL |
|     4400.00 |            10 |
|    13000.00 |            20 |
|    11000.00 |            30 |
|     6500.00 |            40 |
|     8200.00 |            50 |
|     9000.00 |            60 |
|    10000.00 |            70 |
|    13500.00 |            80 |
|    17000.00 |            90 |
|     9000.00 |           100 |
+-------------+---------------+
11 rows in set (0.00 sec)
【查询有奖金的每个领导手下员工的平均工资】
mysql> SELECT AVG(salary),manager_id
    -> FROM employees
    -> WHERE commission_pct IS NOT NULL
    -> GROUP BY manager_id;
+--------------+------------+
| AVG(salary)  | manager_id |
+--------------+------------+
| 12200.000000 |        100 |
|  8500.000000 |        145 |
|  8500.000000 |        146 |
|  7766.666667 |        147 |
|  8650.000000 |        148 |
|  8333.333333 |        149 |
+--------------+------------+
6 rows in set (0.00 sec)
```

### 3.7.4 添加分组后筛选【having】

```sql
【查询哪个部门的员工个数>5】
mysql> SELECT COUNT(*),department_id
    -> FROM employees
    ->
    -> GROUP BY department_id
    ->
    -> HAVING COUNT(*)>5;
+----------+---------------+
| COUNT(*) | department_id |
+----------+---------------+
|        6 |            30 |
|       45 |            50 |
|       34 |            80 |
|        6 |           100 |
+----------+---------------+
4 rows in set (0.00 sec)
【每个工种有奖金的员工的最高工资>12000的工种编号和最高工资】
mysql> SELECT job_id,MAX(salary)
    -> FROM employees
    -> WHERE commission_pct IS NOT NULL
    -> GROUP BY job_id
    -> HAVING MAX(salary)>12000;
+--------+-------------+
| job_id | MAX(salary) |
+--------+-------------+
| SA_MAN |    14000.00 |
+--------+-------------+
1 row in set (0.00 sec)
【领导编号>102的每个领导手下的最低工资大于5000的领导编号和最低工资】
mysql> SELECT manager_id,MIN(salary) minsalary FROM employees WHERE manager_id > 102 GROUP BY manager_id HAVING minsalary > 5000;
+------------+-----------+
| manager_id | minsalary |
+------------+-----------+
|        108 |   6900.00 |
|        145 |   7000.00 |
|        146 |   7000.00 |
|        147 |   6200.00 |
|        148 |   6100.00 |
|        149 |   6200.00 |
|        201 |   6000.00 |
|        205 |   8300.00 |
+------------+-----------+
8 rows in set (0.00 sec)
```

### 3.7.5 按表达式或函数分组

```sql
【按员工姓名的长度分组，查询每一组的员工个数，筛选员工个数>5的有哪些】
mysql> SELECT COUNT(*),LENGTH(last_name) len_name
    -> FROM employees
    -> GROUP BY LENGTH(last_name)
    -> HAVING COUNT(*)>5;
+----------+----------+
| COUNT(*) | len_name |
+----------+----------+
|       11 |        4 |
|       29 |        5 |
|       28 |        6 |
|       15 |        7 |
|        7 |        8 |
|        8 |        9 |
+----------+----------+
6 rows in set (0.00 sec)
```
### 3.7.6 按多个字段分组

```sql
【查询每个工种每个部门的最低工资,并按最低工资降序】
mysql> SELECT MIN(salary),job_id,department_id
    -> FROM employees
    -> GROUP BY department_id,job_id
    -> ORDER BY MIN(salary) DESC;
+-------------+------------+---------------+
| MIN(salary) | job_id     | department_id |
+-------------+------------+---------------+
|    24000.00 | AD_PRES    |            90 |
|    17000.00 | AD_VP      |            90 |
|    13000.00 | MK_MAN     |            20 |
|    12000.00 | AC_MGR     |           110 |
|    12000.00 | FI_MGR     |           100 |
|    11000.00 | PU_MAN     |            30 |
|    10500.00 | SA_MAN     |            80 |
|    10000.00 | PR_REP     |            70 |
|     8300.00 | AC_ACCOUNT |           110 |
|     7000.00 | SA_REP     |          NULL |
|     6900.00 | FI_ACCOUNT |           100 |
|     6500.00 | HR_REP     |            40 |
|     6100.00 | SA_REP     |            80 |
|     6000.00 | MK_REP     |            20 |
|     5800.00 | ST_MAN     |            50 |
|     4400.00 | AD_ASST    |            10 |
|     4200.00 | IT_PROG    |            60 |
|     2500.00 | PU_CLERK   |            30 |
|     2500.00 | SH_CLERK   |            50 |
|     2100.00 | ST_CLERK   |            50 |
+-------------+------------+---------------+
20 rows in set (0.00 sec)
```

### 3.7.7 添加排序

```sql
【每个工种有奖金的员工的最高工资>6000的工种编号和最高工资,按最高工资升序】
mysql> SELECT job_id,MAX(salary) m
    -> FROM employees
    -> WHERE commission_pct IS NOT NULL
    -> GROUP BY job_id
    -> HAVING m>6000
    -> ORDER BY m ;
+--------+----------+
| job_id | m        |
+--------+----------+
| SA_REP | 11500.00 |
| SA_MAN | 14000.00 |
+--------+----------+
2 rows in set (0.00 sec)
```

## 3.8 连接查询	 	★
### 3.8.1 介绍
又称多表查询，当查询的字段来自于多个表时，就会用到连接查询
### 3.8.2 笛卡尔乘积

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/8、笛卡尔乘积现象.png"/> </div>

* 笛卡尔乘积现象：表1 有m行，表2有n行，结果=m*n行
* 发生原因：没有有效的连接条件
* 如何避免：添加有效的连接条件

### 3.8.3 连接查询的分类
#### 3.8.3.1 按年代分类
* sql92标准:仅仅支持内连接
* sql99标准【推荐】：支持内连接+外连接（左外和右外）+交叉连接

#### 3.8.3.2 按功能分类
* 内连接：等值连接；非等值连接；自连接
* 外连接：；左外连接；右外连接；全外连接
* 交叉连接

### 3.8.4 sql92标准
#### 3.8.4.1 等值连接
* 多表等值连接的结果为多表的交集部分
* n表连接，至少需要n-1个连接条件
* 多表的顺序没有要求
* 一般需要为表起别名
* 可以搭配前面介绍的所有子句使用，比如排序、分组、筛选
* 为表起别名<br>

①提高语句的简洁度<br>
②区分多个重名的字段<br>
注意：如果为表起了别名，则查询的字段就不能使用原来的表名去限定<br>

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/9、起别名报错.png"/> </div>

```sql
【查询女神名和对应的男神名】
mysql> SELECT NAME,boyName
    -> FROM boys,beauty
    -> WHERE beauty.boyfriend_id= boys.id;
+------------+---------+
| NAME       | boyName |
+------------+---------+
| 周芷若        | 张无忌       |
| 小昭          | 张无忌       |
| 赵敏          | 张无忌       |
| 热巴          | 鹿晗       |
| Angelababy   | 黄晓明        |
| 王语嫣        | 段誉        |
+------------+---------+
6 rows in set (0.01 sec)
【加筛选：查询有奖金的员工名、部门名】
mysql> SELECT last_name,department_name,commission_pct
    ->
    -> FROM employees e,departments d
    -> WHERE e.`department_id`=d.`department_id`
    -> AND e.`commission_pct` IS NOT NULL limit 5;
+-----------+-----------------+----------------+
| last_name | department_name | commission_pct |
+-----------+-----------------+----------------+
| Russell   | Sal             |           0.40 |
| Partners  | Sal             |           0.30 |
| Errazuriz | Sal             |           0.30 |
| Cambrault | Sal             |           0.30 |
| Zlotkey   | Sal             |           0.20 |
+-----------+-----------------+----------------+
5 rows in set (0.00 sec)
【加分组】
```

#### 3.8.4.2 非等值连接

```sql
【查询员工的工资和工资级别】
mysql> SELECT salary,grade_level
    -> FROM employees e,job_grades g
    -> WHERE salary BETWEEN g.`lowest_sal` AND g.`highest_sal` limit 5;
+----------+-------------+
| salary   | grade_level |
+----------+-------------+
| 24000.00 | E           |
| 17000.00 | E           |
| 17000.00 | E           |
|  9000.00 | C           |
|  6000.00 | C           |
+----------+-------------+
5 rows in set (0.00 sec)
```

#### 3.8..4.3 自连接
把一张表中的自我查找想成是一张表加上另一张表的查找，只不过另一张表还是本身这张表

```sql
【查询 员工名和上级的名称】
mysql> SELECT e.employee_id,e.last_name,m.employee_id,m.last_name
    -> FROM employees e,employees m
    -> WHERE e.`manager_id`=m.`employee_id` limit 5;
+-------------+-----------+-------------+-----------+
| employee_id | last_name | employee_id | last_name |
+-------------+-----------+-------------+-----------+
|         101 | Kochhar   |         100 | K_ing     |
|         102 | De Haan   |         100 | K_ing     |
|         103 | Hunold    |         102 | De Haan   |
|         104 | Ernst     |         103 | Hunold    |
|         105 | Austin    |         103 | Hunold    |
+-------------+-----------+-------------+-----------+
5 rows in set (0.00 sec)

```

### 3.8.5 sql99标准
#### 3.8.5.1 语法
select 查询列表<br>
from 表1 别名 【连接类型】<br>
join 表2 别名 <br>
on 连接条件<br>
【where 筛选条件】<br>
【group by 分组】<br>
【having 筛选条件】<br>
【order by 排序列表】<br>

* 分类：
* 内连接（★）：inner
* 外连接
	* 左外(★):left 【outer】
	* 右外(★)：right 【outer】
	* 全外：full【outer】
* 交叉连接：cross 

#### 3.8.5.2 内连接
* 等值连接

```sql
【查询员工名、部门名】
mysql> SELECT last_name,department_name
    -> FROM departments d
    ->  JOIN  employees e
    -> ON e.`department_id` = d.`department_id` limit 5;
+-----------+-----------------+
| last_name | department_name |
+-----------+-----------------+
| Whalen    | Adm             |
| Hartstein | Mar             |
| Fay       | Mar             |
| Raphaely  | Pur             |
| Khoo      | Pur             |
+-----------+-----------------+
5 rows in set (0.00 sec)
【查询名字中包含e的员工名和工种名（添加筛选）】
mysql> SELECT last_name,job_title
    -> FROM employees e
    -> INNER JOIN jobs j
    -> ON e.`job_id`=  j.`job_id`
    -> WHERE e.`last_name` LIKE '%e%' LIMIT 5;
+-----------+-------------------------------+
| last_name | job_title                     |
+-----------+-------------------------------+
| Gietz     | Public Accountant             |
| Whalen    | Administration Assistant      |
| De Haan   | Administration Vice President |
| Faviet    | Accountant                    |
| Chen      | Accountant                    |
+-----------+-------------------------------+
5 rows in set (0.00 sec)
```

* 非等值连接

```sql
【查询工资级别的个数>20的个数，并且按工资级别降序】
mysql> SELECT COUNT(*),grade_level
    -> FROM employees e
    ->  JOIN job_grades g
    ->  ON e.`salary` BETWEEN g.`lowest_sal` AND g.`highest_sal`
    ->  GROUP BY grade_level
    ->  HAVING COUNT(*)>20
    ->  ORDER BY grade_level DESC LIMIT 5;
+----------+-------------+
| COUNT(*) | grade_level |
+----------+-------------+
|       38 | C           |
|       26 | B           |
|       24 | A           |
+----------+-------------+
3 rows in set (0.00 sec)
```

* 自连接

```sql
【查询员工的名字、上级的名字】
mysql>  SELECT e.last_name,m.last_name
    ->  FROM employees e
    ->  JOIN employees m
    ->  ON e.`manager_id`= m.`employee_id` limit 5;
+-----------+-----------+
| last_name | last_name |
+-----------+-----------+
| Kochhar   | K_ing     |
| De Haan   | K_ing     |
| Hunold    | De Haan   |
| Ernst     | Hunold    |
| Austin    | Hunold    |
+-----------+-----------+
5 rows in set (0.00 sec)
```

#### 3.8.5.3 外连接
* 应用场景：用于查询一个表中有，另一个表没有的记录

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/10、外连接.png"/> </div>

* 特点：<br>
1、外连接的查询结果为主表中的所有记录<br>
如果从表中有和它匹配的，则显示匹配的值<br>
如果从表中没有和它匹配的，则显示null<br>
外连接查询结果=内连接结果+主表中有而从表没有的记录<br>

2、左外连接，left join左边的是主表<br>
右外连接，right join右边的是主表<br>
3、左外和右外交换两个表的顺序，可以实现同样的效果 <br>
4、全外连接=内连接的结果+表1中有但表2没有的+表2中有但表1没有的<br>

```sql
【查询男朋友 不在男神表的的女神名】
【使用id，因为id是主键，不能为空，这样就不会选漏或多选】
mysql> SELECT b.name
    -> FROM beauty b LEFT JOIN boys bo
    -> ON b.`boyfriend_id` = bo.`id`
    -> WHERE bo.`id` IS NULL;
+--------+
| name   |
+--------+
| 柳岩       |
| 苍老师      |
| 周冬雨      |
| 岳灵珊      |
| 双儿      |
| 夏雪      |
+--------+
6 rows in set (0.00 sec)
【查询哪个部门没有员工】
mysql> SELECT d.*,e.employee_id
    ->  FROM departments d
    ->  LEFT OUTER JOIN employees e
    ->  ON d.`department_id` = e.`department_id`
    ->  WHERE e.`employee_id` IS NULL limit 5;
+---------------+-----------------+------------+-------------+-------------+
| department_id | department_name | manager_id | location_id | employee_id |
+---------------+-----------------+------------+-------------+-------------+
|           120 | Tre             |       NULL |        1700 |        NULL |
|           130 | Cor             |       NULL |        1700 |        NULL |
|           140 | Con             |       NULL |        1700 |        NULL |
|           150 | Sha             |       NULL |        1700 |        NULL |
|           160 | Ben             |       NULL |        1700 |        NULL |
+---------------+-----------------+------------+-------------+-------------+
5 rows in set (0.00 sec)
```

#### 3.8.5.4 全外连接【不支持】

```sql
 SELECT b.*,bo.*
 FROM beauty b
 FULL OUTER JOIN boys bo
 ON b.`boyfriend_id` = bo.id;
```

#### 3.8.5.5 交叉连接【笛卡尔积】
## 3.9 子查询       √
### 3.9.1 含义
* 出现在其他语句中的select语句，称为子查询或内查询
* 外部的查询语句，称为主查询或外查询

### 3.9.2 分类
#### 3.9.2.1 按子查询出现的位置
* select后面：仅仅支持标量子查询
* from后面：支持表子查询
* where或having后面：★标量子查询（单行） √；列子查询  （多行） √；行子查询
* exists后面（相关子查询）：表子查询
#### 3.9.2.2 按结果集的行列数不同
* 标量子查询（结果集只有一行一列）
* 列子查询（结果集只有一列多行）
* 行子查询（结果集有一行多列）
* 表子查询（结果集一般为多行多列）

### 3.9.3 where或having后面
* 1、标量子查询（单行子查询）
* 2、列子查询（多行子查询）
* 3、行子查询（多列多行）

* 特点：<br>
①子查询放在小括号内<br>
②子查询一般放在条件的右侧<br>
③标量子查询，一般搭配着单行操作符使用：> < >= <= = <><br>
列子查询，一般搭配着多行操作符使用：in、any/some、all<br>
④子查询的执行优先于主查询执行，主查询的条件用到了子查询的结果<br>

#### 3.9.3.1 标量子查询

```sql
【谁的工资比 Abel 高?】
mysql> SELECT *
    -> FROM employees
    -> WHERE salary>(
    ->
    -> SELECT salary
    -> FROM employees
    -> WHERE last_name = 'Abel'
    ->
    -> ) limit 5;
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number       | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567       | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568       | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569       | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         108 | Nancy      | Greenberg | NGREENBE | 515.124.4569       | FI_MGR  | 12000.00 |           NULL |        101 |           100 | 1998-03-03 00:00:00 |
|         145 | John       | Russell   | JRUSSEL  | 011.44.1344.429268 | SA_MAN  | 14000.00 |           0.40 |        100 |            80 | 2002-12-23 00:00:00 |
+-------------+------------+-----------+----------+--------------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```

#### 3.9.3.2 列子查询
* IN/NOT IN：等于列表中的 任意一个【只要列表中有一个即可】
* ANY|SOME：和子查询返回的 某一个 值比较【比如大于或者小于列表中的一个值即可，可用min或者max代替】
* ALL：和子查询返回的所有值比较

```sql
【返回location_id是1400或1700的部门中的所有员工姓名】
mysql> SELECT last_name
    -> FROM employees
    -> WHERE department_id  IN(
    -> SELECT DISTINCT department_id
    -> FROM departments
    -> WHERE location_id IN(1400,1700)
    -> ) LIMIT 5;
+-----------+
| last_name |
+-----------+
| K_ing     |
| Kochhar   |
| De Haan   |
| Hunold    |
| Ernst     |
+-----------+
5 rows in set (0.00 sec)
```

#### 3.9.3.3 行子查询

```sql
【查询员工编号最小并且工资最高的员工信息】
mysql> SELECT *
    -> FROM employees
    -> WHERE (employee_id,salary)=(
    -> SELECT MIN(employee_id),MAX(salary)
    -> FROM employees
    -> );
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+-------+--------------+---------+----------+----------------+------------+---------------+---------------------+
1 row in set (0.00 sec)
```

#### 3.9.3.4 select后面的子查询

```sql
【查询每个部门的员工个数】
mysql> SELECT d.*,(
    ->
    -> SELECT COUNT(*)
    -> FROM employees e
    -> WHERE e.department_id = d.`department_id`
    ->  ) 个数
    ->  FROM departments d;
+---------------+-----------------+------------+-------------+------+
| department_id | department_name | manager_id | location_id | 个数     |
+---------------+-----------------+------------+-------------+------+
|            10 | Adm             |        200 |        1700 |    1 |
|            20 | Mar             |        201 |        1800 |    2 |
|            30 | Pur             |        114 |        1700 |    6 |
|            40 | Hum             |        203 |        2400 |    1 |
|            50 | Shi             |        121 |        1500 |   45 |
|            60 | IT              |        103 |        1400 |    5 |
|            70 | Pub             |        204 |        2700 |    1 |
|            80 | Sal             |        145 |        2500 |   34 |
|            90 | Exe             |        100 |        1700 |    3 |
|           100 | Fin             |        108 |        1700 |    6 |
|           110 | Acc             |        205 |        1700 |    2 |
|           120 | Tre             |       NULL |        1700 |    0 |
|           130 | Cor             |       NULL |        1700 |    0 |
|           140 | Con             |       NULL |        1700 |    0 |
|           150 | Sha             |       NULL |        1700 |    0 |
|           160 | Ben             |       NULL |        1700 |    0 |
|           170 | Man             |       NULL |        1700 |    0 |
|           180 | Con             |       NULL |        1700 |    0 |
|           190 | Con             |       NULL |        1700 |    0 |
|           200 | Ope             |       NULL |        1700 |    0 |
|           210 | IT              |       NULL |        1700 |    0 |
|           220 | NOC             |       NULL |        1700 |    0 |
|           230 | IT              |       NULL |        1700 |    0 |
|           240 | Gov             |       NULL |        1700 |    0 |
|           250 | Ret             |       NULL |        1700 |    0 |
|           260 | Rec             |       NULL |        1700 |    0 |
|           270 | Pay             |       NULL |        1700 |    0 |
+---------------+-----------------+------------+-------------+------+
27 rows in set (0.00 sec)
```

#### 3.9.3.5 from后面的子查询

将子查询结果充当一张表，要求必须起别名

```sql
【查询每个部门的平均工资的工资等级】
mysql> SELECT  ag_dep.*,g.`grade_level`
    -> FROM (
    -> SELECT AVG(salary) ag,department_id
    -> FROM employees
    -> GROUP BY department_id
    -> ) ag_dep
    -> INNER JOIN job_grades g
    -> ON ag_dep.ag BETWEEN lowest_sal AND highest_sal LIMIT 5;
+-------------+---------------+-------------+
| ag          | department_id | grade_level |
+-------------+---------------+-------------+
| 7000.000000 |          NULL | C           |
| 4400.000000 |            10 | B           |
| 9500.000000 |            20 | C           |
| 4150.000000 |            30 | B           |
| 6500.000000 |            40 | C           |
+-------------+---------------+-------------+
5 rows in set (0.00 sec)
```

#### 3.9.3.6 exits后面的子查询【相关子查询】
* 语法：<br>
exists(完整的查询语句)<br>
结果：1(true)或0(false)

```sql
【查询有员工的部门名】
SELECT department_name
FROM departments d
WHERE EXISTS(
	SELECT *
	FROM employees e
	WHERE d.`department_id`=e.`department_id`


);
```

## 3.10 分页查询       ★
### 3.10.1 语法
select 查询列表<br>
from 表<br>
【join type join 表2<br>
on 连接条件<br>
where 筛选条件<br>
group by 分组字段<br>
having 分组后的筛选<br>
order by 排序的字段】<br>
limit 【offset,】size;<br>

offset要显示条目的起始索引（起始索引从0开始）<br>
size 要显示的条目个数<br>

* 应用场景：当要显示的数据，一页显示不全，需要分页提交sql请求
	

特点：
①limit语句放在查询语句的最后
②公式
要显示的页数 page，每页的条目数size

select 查询列表
from 表
limit (page-1)*size,size;

size=10
page  
1	0
2  	10
3	20
	
### 3.10.2 示例

```sql
【查询前五条员工信息】
【起始位置从0开始，可以省略】
mysql> SELECT * FROM  employees LIMIT 0,5;
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         100 | Steven     | K_ing     | SKING    | 515.123.4567 | AD_PRES | 24000.00 |           NULL |       NULL |            90 | 1992-04-03 00:00:00 |
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG |  6000.00 |           NULL |        103 |            60 | 1992-04-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)
```

## 3.11 union联合查询	√
* 将多条查询语句的结果合并成一个结果
* 语法：<br>
查询语句1<br>
union<br>
查询语句2<br>
union<br>
...<br>

* 应用场景：要查询的结果来自于多个表，且多个表没有直接的连接关系，但查询的信息一致时

* 特点：★<br>
1、要求多条查询语句的查询列数是一致的！<br>
2、要求多条查询语句的查询的每一列的类型和顺序最好一致<br>
3、union关键字默认去重，如果使用union all 可以包含重复项<br>

```sql
【查询部门编号>90或邮箱包含a的员工信息】
mysql> SELECT * FROM employees  WHERE email LIKE '%a%'
    -> UNION
    -> SELECT * FROM employees  WHERE department_id>90 limit 5;
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
| employee_id | first_name | last_name | email    | phone_number | job_id  | salary   | commission_pct | manager_id | department_id | hiredate            |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
|         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |           NULL |        100 |            90 | 1992-04-03 00:00:00 |
|         103 | Alexander  | Hunold    | AHUNOLD  | 590.423.4567 | IT_PROG |  9000.00 |           NULL |        102 |            60 | 1992-04-03 00:00:00 |
|         105 | David      | Austin    | DAUSTIN  | 590.423.4569 | IT_PROG |  4800.00 |           NULL |        103 |            60 | 1998-03-03 00:00:00 |
|         106 | Valli      | Pataballa | VPATABAL | 590.423.4560 | IT_PROG |  4800.00 |           NULL |        103 |            60 | 1998-03-03 00:00:00 |
+-------------+------------+-----------+----------+--------------+---------+----------+----------------+------------+---------------+---------------------+
5 rows in set (0.00 sec)

【查询中国用户中男性的信息以及外国用户中年男性的用户信息】
SELECT id,cname FROM t_ca WHERE csex='男'
UNION ALL
SELECT t_id,tname FROM t_ua WHERE tGender='male';
```

# 四、DML语言的学习    ★ 
## 4.1 插入语句	
### 4.1.1 第一种方式
* 语法：insert into 表名(列名,...) values(值1,...);
* 列的顺序可以调换
* 列数和值的个数必须一致
* 插入的值的类型要与列的类型一致或兼容

```sql
INSERT INTO beauty(id,NAME,sex,borndate,phone,photo,boyfriend_id)
VALUES(13,'唐艺昕','女','1990-4-23','1898888888',NULL,2);
```

* 不可以 为null 的列必须插入值。可以 为null 的列如何插入值？

```sql
#方式一：
INSERT INTO beauty(id,NAME,sex,borndate,phone,photo,boyfriend_id)
VALUES(13,'唐艺昕','女','1990-4-23','1898888888',NULL,2);

#方式二：【去掉可以为空的列】

INSERT INTO beauty(id,NAME,sex,phone)
VALUES(15,'娜扎','女','1388888888');
```

* 可以省略列名，默认所有列，而且列的顺序和表中列的顺序一致

```sql
INSERT INTO beauty
VALUES(18,'张飞','男',NULL,'119',NULL,NULL);
```

### 4.1.2 第二种方式
* 语法：insert into 表名 set 列名=值,列名=值,...

```sql
INSERT INTO beauty
SET id=19,NAME='刘涛',phone='999';
```

### 4.1.3 两种方式比较
* 方式一支持插入多行,方式二不支持
* 方式一支持子查询，方式二不支持

```sql
INSERT INTO beauty(id,NAME,phone)
SELECT 26,'宋茜','11809866';

INSERT INTO beauty(id,NAME,phone)
SELECT id,boyname,'1234567'
FROM boys WHERE id<3;
```

## 4.2 修改语句	
### 4.2.1 修改单表的记录★
* 语法：update 表名 set 列=新值,列=新值,...  where 筛选条件;

```sql
【修改beauty表中姓唐的女神的电话为13899888899】

UPDATE beauty SET phone = '13899888899'
WHERE NAME LIKE '唐%';
```

### 4.2.2 修改多表的记录【补充】

* sql92语法：<br>
update 表1 别名,表2 别名<br>
set 列=值,...<br>
where 连接条件<br>
and 筛选条件;<br>

* sql99语法：<br>
update 表1 别名<br>
inner|left|right join 表2 别名<br>
on 连接条件<br>
set 列=值,...<br>
where 筛选条件;<br>

```sql
【修改张无忌的女朋友的手机号为114】
UPDATE boys bo
INNER JOIN beauty b ON bo.`id`=b.`boyfriend_id`
SET b.`phone`='119',bo.`userCP`=1000
WHERE bo.`boyName`='张无忌';

【修改没有男朋友的女神的男朋友编号都为2号】
UPDATE boys bo
RIGHT JOIN beauty b ON bo.`id`=b.`boyfriend_id`
SET b.`boyfriend_id`=2
WHERE bo.`id` IS NULL;
```

## 4.3 删除语句	
### 4.3.1 delete
#### 4.3.1.1 单表的删除【★】
* 语法：delete from 表名 where 筛选条件

```sql
【删除手机号以9结尾的女神信息】

DELETE FROM beauty WHERE phone LIKE '%9';
```

#### 4.3.1.2 多表的删除【补充】

* sql92语法：<br>
delete 表1的别名,表2的别名<br>
from 表1 别名,表2 别名<br>
where 连接条件<br>
and 筛选条件;<br>

* sql99语法：<br>
delete 表1的别名,表2的别名<br>
from 表1 别名<br>
inner|left|right join 表2 别名 on 连接条件<br>
where 筛选条件;<br>

```sql
【删除张无忌的女朋友的信息】

DELETE b
FROM beauty b
INNER JOIN boys bo ON b.`boyfriend_id` = bo.`id`
WHERE bo.`boyName`='张无忌';

【删除黄晓明的信息以及他女朋友的信息】
DELETE b,bo
FROM beauty b
INNER JOIN boys bo ON b.`boyfriend_id`=bo.`id`
WHERE bo.`boyName`='黄晓明';

```

### 4.3.2 truncate【清空表数据】
* 语法：truncate table 表名;

# 五、DDL语言的学习  

## 5.1 库的管理	 √
### 5.1.1 库的创建
* 语法：create database  [if not exists]库名;

```sql
【创建库Books】
CREATE DATABASE IF NOT EXISTS books ;
```

### 5.1.2 库的修改
* 语法：RENAME DATABASE books TO 新库名;
* 更改库的字符集：ALTER DATABASE books CHARACTER SET gbk;

### 5.1.3 库的删除
* DROP DATABASE IF EXISTS books;

## 5.2 表的管理	 √
### 5.2.1 表的创建 ★
* 语法：
create table 表名(<br>
	列名 列的类型【(长度) 约束】,<br>
	列名 列的类型【(长度) 约束】,<br>
	列名 列的类型【(长度) 约束】,<br>
	...<br>
	列名 列的类型【(长度) 约束】<br>
	)<br>
	
```sql
【创建表Book】
CREATE TABLE book(
	id INT,#编号
	bName VARCHAR(20),#图书名
	price DOUBLE,#价格
	authorId  INT,#作者编号
	publishDate DATETIME#出版日期
);
DESC book;【查看表结构】
```

### 5.2.2 表的修改
* 语法：alter table 表名 add|drop|modify|change column 列名 【列类型 约束】;

```sql
【修改列名】
【将publishdate列名修改为pubDate】
ALTER TABLE book CHANGE COLUMN publishdate pubDate DATETIME;
【修改列的类型或约束】
ALTER TABLE book MODIFY COLUMN pubdate TIMESTAMP;
【添加新列】
ALTER TABLE author ADD COLUMN annual DOUBLE; 
【删除列】
ALTER TABLE book_author DROP COLUMN  annual;
【修改表名】
ALTER TABLE author RENAME TO book_author;
```

### 5.2.3 表的删除
* DROP TABLE IF EXISTS book_author;
* 通用的写法：<br>

DROP DATABASE IF EXISTS 旧库名;<br>
CREATE DATABASE 新库名;<br>


DROP TABLE IF EXISTS 旧表名;<br>
CREATE TABLE  表名();<br>

### 5.2.4 表的复制

```sql
【仅仅复制表的结构】
CREATE TABLE copy LIKE author;

【复制表的结构+数据】
CREATE TABLE copy2 
SELECT * FROM author;

【只复制部分数据】
CREATE TABLE copy3
SELECT id,au_name
FROM author 
WHERE nation='中国';


【仅仅复制某些字段】

CREATE TABLE copy4 
SELECT id,au_name
FROM author
WHERE 0;
```

## 5.3 常见数据类型介绍  √ 
### 5.3.1 分类
* 数值型：整型、小数【定点数、浮点数】
* 字符型：较短的文本：char、varchar；较长的文本：text、blob（较长的二进制数据）
* 日期型：

### 5.3.2 整型

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/11、整型.png"/> </div>

* 特点：<br>
① 如果不设置无符号还是有符号，默认是有符号，如果想设置无符号，需要添加unsigned关键字<br>
② 如果插入的数值超出了整型的范围,会报out of range异常，并且插入临界值<br>
③ 如果不设置长度，会有默认的长度<br>
长度代表了显示的最大宽度，如果不够会用0在左边填充，但必须搭配zerofill使用！<br>
加上zerofill默认无符号

```sql
【设置无符号和有符号】
CREATE TABLE tab_int(
	t1 INT,
	t2 INT UNSIGNED 
	t3 INT ZEROFILL
);

```

### 5.3.3 小数

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/12、小数.png"/> </div>

* 1.浮点型<br>
float(M,D)<br>
double(M,D)<br>

* 2.定点型<br>
dec(M，D)<br>
decimal(M,D)【两个写法一样作用】<br>

* 特点：

①<br>
M：整数部位+小数部位<br>
D：小数部位<br>
如果超过范围，则插入临界值<br>

```sql
CREATE TABLE tab_float(
	f1 FLOAT(5,2),
	f2 DOUBLE(5,2),
	f3 DECIMAL(5,2)
);
INSERT INTO tab_float VALUES(123.45,123.45,123.45);
INSERT INTO tab_float VALUES(123.456,123.456,123.456);
INSERT INTO tab_float VALUES(123.4,123.4,123.4);
INSERT INTO tab_float VALUES(1523.4,1523.4,1523.4);
-------------------------------------------------------------
mysql> select * from tab_float;
+--------+--------+--------+
| f1     | f2     | f3     |
+--------+--------+--------+
| 123.45 | 123.45 | 123.45 |
| 123.46 | 123.46 | 123.46 |【四舍五入】
| 123.40 | 123.40 | 123.40 |【不足补0】
| 999.99 | 999.99 | 999.99 |【超出填入临界值】
+--------+--------+--------+
4 rows in set (0.00 sec)

```

②<br>
M和D都可以省略<br>
如果是decimal，则M默认为10，D默认为0<br>
如果是float和double，则会根据插入的数值的精度来决定精度<br>

③定点型的精确度较高，如果要求插入数值的精度较高如货币运算等则考虑使用<br>

```sql
CREATE TABLE tab_float1(
	f1 FLOAT,
	f2 DOUBLE,
	f3 DECIMAL
);

INSERT INTO tab_float1 VALUES(123.4523,123.4523,123.4523);
INSERT INTO tab_float1 VALUES(123.456,123.456,123.456);
INSERT INTO tab_float1 VALUES(123.4,123.4,123.4);
INSERT INTO tab_float1 VALUES(1523.4,1523.4,1523.4);
----------------------------------------------
mysql> select * from tab_float1;
+---------+----------+------+
| f1      | f2       | f3   |
+---------+----------+------+
| 123.452 | 123.4523 |  123 |
| 123.456 |  123.456 |  123 |
|   123.4 |    123.4 |  123 |
|  1523.4 |   1523.4 | 1523 |
+---------+----------+------+
4 rows in set (0.00 sec)
```

### 5.3.4 字符型

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/14、字符类型.png"/> </div>

较短的文本：<br>

char<br>
varchar<br>

其他：<br>

binary和varbinary用于保存较短的二进制<br>
enum用于保存枚举,要求插入的值必须属于列表中指定的值之一。如果列表成员为1\~255，则需要1个字节存储；如果列表成员为255\~65535，则需要2个字节存储；最多需要65535个成员！<br>

```sql
CREATE TABLE tab_char(
	c1 ENUM('a','b','c')
);

INSERT INTO tab_char VALUES('a');
INSERT INTO tab_char VALUES('b');
INSERT INTO tab_char VALUES('c');
INSERT INTO tab_char VALUES('m');【不成功】
INSERT INTO tab_char VALUES('A');

SELECT * FROM tab_char;
```

set用于保存集合。和 说明：和Enum 类型类似，里面可以保存0~64 个成员。和Enum 类型最大的区： 别是：SET 类型一次可以选取多个成员，而Enum 只能选一个<br>
根据成员个数不同，存储所占的字节也不同<br>

<table>
<thead>
<tr>
<th>成员数</th>
<th>字节数</th>
</tr>
</thead>
<tbody>
<tr>
<th>1~8</th>
<th>1</th>
</tr>
<tr>
<th>9~16</th>
<th>2</th>
</tr>
<tr>
<th>17~24</th>
<th>3</th>
</tr>
<tr>
<th>25~32 </th>
<th>4</th>
</tr>
<tr>
<th>33~64</th>
<th>8</th>
</tr>
</tbody>
</table>

```sql
CREATE TABLE tab_set(
	s1 SET('a','b','c','d')
);
INSERT INTO tab_set VALUES('a');
INSERT INTO tab_set VALUES('A,B');
INSERT INTO tab_set VALUES('a,c,d');
```

较长的文本：<br>
text<br>
blob(较大的二进制)<br>

<table>
<thead>
<tr>
<th></th>
<th>写法</th>
<th>M的意思</th>
<th>特点</th>
<th>空间的耗费</th>
<th>效率</th>
</tr>
</thead>
<tbody>
<tr>
<th>char</th>
<th>char(M)</th>
<th>最大的字符数，可以省略，默认为1</th>
<th>固定长度的字符</th>
<th>比较耗费</th>
<th>高</th>
</tr>
<tr>
<th>varchar</th>
<th>varchar(M)</th>
<th>最大的字符数，不可以省略</th>
<th>可变长度的字符</th>
<th>比较节省</th>
<th>低</th>
</tr>
</tbody>
</table>

### 5.3.5 日期型

<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/15、日期类型.png"/> </div>

* timestamp和实际时区有关，更能反映实际的日期，而datetime则只能反映出插入时的当地时区

```sql
CREATE TABLE tab_date(
	t1 DATETIME,
	t2 TIMESTAMP
);

INSERT INTO tab_date VALUES(NOW(),NOW());
SELECT * FROM tab_date;

SHOW VARIABLES LIKE 'time_zone';
SET time_zone='+9:00';【修改时区】
【在查看两个时间，发现DATETIME的时间没变化，TIMESTAMP的时间增加了一个小时】
```

## 5.4 常见约束  	  √	
### 5.4.1 含义
* 一种限制，用于限制表中的数据，为了保证表中的数据的准确和可靠性

### 5.4.2 分类【六大分类】
* NOT NULL：非空，用于保证该字段的值不能为空。比如姓名、学号等
* DEFAULT:默认，用于保证该字段有默认值。比如性别
* PRIMARY KEY:主键，用于保证该字段的值具有唯一性，并且非空。比如学号、员工编号等
* UNIQUE:唯一，用于保证该字段的值具有唯一性，可以为空。比如座位号
* CHECK:检查约束【mysql中不支持】。比如年龄、性别
* FOREIGN KEY:外键，用于限制两个表的关系，用于保证该字段的值必须来自于主表的关联列的值。在从表添加外键约束，用于引用主表中某列的值。比如学生表的专业编号，员工表的部门编号，员工表的工种编号<br>

* 添加约束的时机：<br>
1.创建表时<br>
2.修改表时<br>

```sql
CREATE TABLE 表名(
	字段名 字段类型 列级约束,
	字段名 字段类型,
	表级约束

)
```

* 约束的添加分类：
	* 列级约束：六大约束语法上都支持，但外键约束没有效果
	* 表级约束：除了非空、默认，其他的都支持
	
### 5.4.3 创建表时添加约束
#### 5.4.3.1 列级约束
* 语法：直接在字段名和类型后面追加 约束类型即可。
* 只支持：默认、非空、主键、唯一

```sql
CREATE TABLE stuinfo(
	id INT PRIMARY KEY,#主键
	stuName VARCHAR(20) NOT NULL UNIQUE,#非空
	gender CHAR(1) CHECK(gender='男' OR gender ='女'),#检查
	seat INT UNIQUE,#唯一
	age INT DEFAULT  18,#默认约束
	majorId INT foreign REFERENCES major(id) #外键【但没有效果】
);
CREATE TABLE major(
	id INT PRIMARY KEY,
	majorName VARCHAR(20)
);
```

* 查看stuinfo中的所有索引，包括主键、外键、唯一：SHOW INDEX FROM stuinfo;

#### 5.4.3.2 表级约束
* 语法：在各个字段的最下面【constraint 约束名】 约束类型(字段名) 

```sql
DROP TABLE IF EXISTS stuinfo;
CREATE TABLE stuinfo(
	id INT,
	stuname VARCHAR(20),
	gender CHAR(1),
	seat INT,
	age INT,
	majorid INT,
	
	CONSTRAINT pk PRIMARY KEY(id),#主键【主键索引名默认改不了，为primary】
	CONSTRAINT uq UNIQUE(seat),#唯一键
	CONSTRAINT ck CHECK(gender ='男' OR gender  = '女'),#检查
	CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERENCES major(id)#外键
);
----------------------------------------------
【通用的写法：★】
CREATE TABLE IF NOT EXISTS stuinfo(
	id INT PRIMARY KEY,
	stuname VARCHAR(20),
	sex CHAR(1),
	age INT DEFAULT 18,
	seat INT UNIQUE,
	majorid INT,
	CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERENCES major(id)

);

```

### 5.4.4 修改表时添加约束
* 1、添加列级约束<br>
alter table 表名 modify column 字段名 字段类型 新约束;

* 2、添加表级约束<br>
alter table 表名 add 【constraint 约束名】 约束类型(字段名) 【外键的引用】;

```sql
DROP TABLE IF EXISTS stuinfo;
CREATE TABLE stuinfo(
	id INT,
	stuname VARCHAR(20),
	gender CHAR(1),
	seat INT,
	age INT,
	majorid INT
)
DESC stuinfo;

【添加非空约束】
ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20)  NOT NULL;
【添加默认约束】
ALTER TABLE stuinfo MODIFY COLUMN age INT DEFAULT 18;
【添加唯一】
#列级约束
ALTER TABLE stuinfo MODIFY COLUMN seat INT UNIQUE;
#表级约束
ALTER TABLE stuinfo ADD UNIQUE(seat);

【添加主键】
#列级约束
ALTER TABLE stuinfo MODIFY COLUMN id INT PRIMARY KEY;
#表级约束
ALTER TABLE stuinfo ADD PRIMARY KEY(id);

【添加外键】
ALTER TABLE stuinfo ADD CONSTRAINT fk_stuinfo_major FOREIGN KEY(majorid) REFERENCES major(id); 
```

### 5.4.5 修改表时删除约束

```sql
#1.删除非空约束
ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20) NULL;

#2.删除默认约束
ALTER TABLE stuinfo MODIFY COLUMN age INT ;

#3.删除主键
ALTER TABLE stuinfo DROP PRIMARY KEY;

#4.删除唯一
ALTER TABLE stuinfo DROP INDEX seat;

#5.删除外键
ALTER TABLE stuinfo DROP FOREIGN KEY fk_stuinfo_major;
```

### 5.4.6 主键和唯一的区别

<table>
<thead>
<tr>
<th></th>
<th>保证唯一性</th>
<th>是否允许为空</th>
<th>一个表中可以有多少个</th>
<th>是否允许组合</th>
</tr>
</thead>
<tbody>
<tr>
<th>主键</th>
<th>√ </th>
<th>×</th>
<th>至多一个主键</th>
<th>√ ，但不推荐</th>
</tr>
<tr>
<th>唯一键</th>
<th>√ </th>
<th>√，但null也只能有一个 </th>
<th>可以有多个唯一键</th>
<th>√ ，但不推荐</th>
</tr>
</tbody>
</table>

### 5.4.7 外键

* 1、要求在从表设置外键关系
* 2、从表的外键列的类型和主表的关联列的类型要求一致或兼容，名称无要求
* 3、主表的关联列必须是一个key（一般是主键或唯一）
* 4、插入数据时，先插入主表，再插入从表
* 删除数据时，先删除从表，再删除主表

## 5.5 标识列【自增长列】
### 5.5.1 介绍
* 含义：可以不用手动的插入值，系统提供默认的序列值
* 特点：<br>
1、标识列必须和主键搭配吗？不一定，但要求是一个key<br>
2、一个表可以有几个标识列？至多一个！<br>
3、标识列的类型只能是数值型<br>
4、标识列可以通过 SET auto_increment_increment=3;设置步长<br>
可以通过 手动插入值，设置起始值<br>
### 5.5.2 示例


```sql
【创建表时设置标识列】
CREATE TABLE tab_identity(
	id INT  ,
	NAME FLOAT UNIQUE AUTO_INCREMENT,
	seat INT 
);
```

# 六、TCL语言的学习
## 6.1 事务的介绍
* 一个或一组sql语句组成一个执行单元，这个执行单元要么全部执行，要么全部不执行。
* **<font color=red size=4>事务由单独单元的一个或多个SQL语句组成，在这个单元中，每个MySQL语句是相互依赖的。</font>**而整个单独单元作为一个不可分割的整体，如果单元中某条SQL语句一旦执行失败或产生错误，整个单元将会回滚。所有受到影响的数据将返回到事物开始以前的状态；如果单元中的所有SQL语句均执行成功，则事物被顺利执行。

## 6.2 事务的特点【ACID】
* **<font color=red size=4>原子性</font>**（Atomicity）：原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。
* **<font color=red size=4>一致性</font>**（Consistency）：事务必须使数据库从一个一致性状态变换到另外一个一致性状态。
* **<font color=red size=4>隔离性</font>**（Isolation）：事务的隔离性是指一个事务的执行不能被其他事务干扰，即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。
* **<font color=red size=4>持久性</font>**（Durability）：持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来的其他操作和数据库故障不应该对其有任何影响

## 6.3 事务的创建
* 隐式事务：事务没有明显的开启和结束的标记。比如insert、update、delete语句
* 显式事务：事务具有明显的开启和结束的标记。前提：必须先设置自动提交功能为禁用<br>
set autocommit=0;<br>
show variables like 'autocommit';【查看autocommit变量属性】<br>

步骤1：开启事务<br>
set autocommit=0;<br>
start transaction;可选的<br>
步骤2：编写事务中的sql语句(select insert update delete)<br>
语句1;<br>
语句2;<br>
...<br>

步骤3：结束事务<br>
commit;提交事务<br>
rollback;回滚事务<br>

savepoint 节点名;设置保存点<br>

## 6.4 事务并发问题
* **<font color=red size=4>脏读</font>**: 对于两个事务 T1, T2, T1 读取了已经被 T2 更新但还 **<font color=blue size=4>没有被提交</font>**的字段.之后, 若 T2 回滚, T1读取的内容就是临时且无效的.
* **<font color=red size=4>不可重复读</font>**: 对于两个事务T1, T2, T1 读取了一个字段, 然后 T2  **<font color=blue size=4> 更新</font>**了该字段.之后, T1再次读取同一个字段, 值就不同了.
* **<font color=red size=4>幻读</font>**: 对于两个事务T1, T2, T1 从一个表中读取了一个字段, 然后 T2 在该表中  **<font color=blue size=4>插入</font>**了一些新的行. 之后, 如果 T1 再次读取同一个表, 就会多出几行.

## 6.5 事务的隔离级别
* 数据库事务的隔离性: 数据库系统必须具有隔离并发运行各个事务的能力,使它们不会相互影响, 避免各种并发问题
* 一个事务与其他事务隔离的程度称为隔离级别。数据库规定了多种事务隔离级别, 不同隔离级别对应不同的干扰程度, 隔离级别越高, 数据一致性就越好, 但并发性越弱.


<div align="center"> <img src="https://cxquang.github.io/BigDataForLearn/_picture/MySQL基础/16、数据库的隔离级别.png"/> </div>

# 七、视图的讲解           √
## 7.1 视图的介绍
* MySQL从5.0.1版本开始提供视图功能。一种虚拟存在的表，行和列的数据来自定义视图的查询中使用的表，并且是在使用视图时 **<font color=red size=4> 动态生成</font>**的，**<font color=blue size=4> 只保存了sql逻辑，不保存查询结果</font>**
* 应用场景：<br>
– 多个地方用到同样的查询结果<br>
– 该查询结果使用的sql语句较复杂<br>

<table>
<thead>
<tr>
<th></th>
<th>创建语法的关键字</th>
<th>是否实际占用了物理空间</th>
<th>使用</th>
</tr>
</thead>
<tbody>
<tr>
<th>视图</th>
<th>create view</th>
<th>只是保存了sql逻辑</th>
<th>增删改查，只是一般不能增删改 </th>
</tr>
<tr>
<th>表</th>
<th>create table </th>
<th>保存了数据 </th>
<th>增删改查</th>
</tr>
</tbody>
</table>

## 7.2 视图的创建
* 语法：create view 视图名 as 查询语句;

```sql
【查询姓名中包含a字符的员工名、部门名和工种信息】
CREATE VIEW myv1
AS
SELECT last_name,department_name,job_title
FROM employees e
JOIN departments d ON e.department_id  = d.department_id
JOIN jobs j ON j.job_id  = e.job_id;

SELECT * FROM myv1 WHERE last_name LIKE '%a%';

【查询各部门的平均工资级别】
CREATE VIEW myv2
AS
SELECT AVG(salary) ag,department_id
FROM employees
GROUP BY department_id;

SELECT myv2.`ag`,g.grade_level
FROM myv2
JOIN job_grades g
ON myv2.`ag` BETWEEN g.`lowest_sal` AND g.`highest_sal`;

【查询平均工资最低的部门信息】
SELECT * FROM myv2 ORDER BY ag LIMIT 1;

【查询平均工资最低的部门名和工资】

CREATE VIEW myv3
AS
SELECT * FROM myv2 ORDER BY ag LIMIT 1;

SELECT d.*,m.ag
FROM myv3 m
JOIN departments d
ON m.`department_id`=d.`department_id`;
```

## 7.3 视图的修改
### 7.3.1 方式一
create or replace view  视图名<br>
as<br>
查询语句;<br>

### 7.3.2 方式二
alter view 视图名<br>
as <br>
查询语句;<br>

## 7.4 视图的删除&查看视图
* drop view 视图名,视图名,...;
* 查看视图：DESC myv3;
* SHOW CREATE VIEW myv3;

## 7.5 视图的更新【会更改原始表】
* 具备以下特点的视图不允许更新<br>
包含以下关键字的sql语句：分组函数、distinct、group  by、having、union或者union all<br>
Select中包含子查询<br>
from一个不能更新的视图<br>
where子句的子查询引用了from子句中的表<br>

```sql
CREATE OR REPLACE VIEW myv1
AS
SELECT last_name,email
FROM employees;
【插入】
INSERT INTO myv1 VALUES('张飞','zf@qq.com');
```

# 八、变量
## 8.1 变量的分类
* 系统变量：
	* 全局变量
	* 会话变量

* 自定义变量：
	* 用户变量
	* 局部变量

## 8.2 系统变量
* 说明：变量由系统定义，不是用户定义，属于服务器层面
* 注意：全局变量需要添加global关键字，会话变量需要添加session关键字，如果不写，默认会话级别
* 使用步骤：<br>
1、查看所有系统变量：show global【session】variables;<br>
2、查看满足条件的部分系统变量：show global【session】 variables like '%char%';<br>
3、查看指定的系统变量的值：select @@global【session】.系统变量名;<br>
4、为某个系统变量赋值<br>
方式一：<br>
set global【session】系统变量名=值;<br>
方式二：<br>
set @@global【session】.系统变量名=值;<br>

## 8.3 自定义变量
* 说明：变量由用户自定义，而不是系统提供的
* 使用步骤：<br>
1、声明<br>
2、赋值<br>
3、使用（查看、比较、运算等）<br>

### 8.3.1 用户变量
* 作用域：针对于当前会话（连接）有效，作用域同于会话变量
* 赋值操作符：=或:=
* 声明并初始化

```sql
SET @变量名=值;
SET @变量名:=值;
SELECT @变量名:=值;
```

* 赋值（更新变量的值）

```sql
#方式一：
	SET @变量名=值;
	SET @变量名:=值;
	SELECT @变量名:=值;
#方式二：
	SELECT 字段 INTO @变量名
	FROM 表;
```

* 使用（查看变量的值）：SELECT @变量名;

### 8.3.2 局部变量
* 作用域：仅仅在定义它的begin end块中有效
* 应用在 begin end中的第一句话

```sql
【声明】
DECLARE 变量名 类型;
DECLARE 变量名 类型 【DEFAULT 值】;


【赋值（更新变量的值）】

#方式一：
	SET 局部变量名=值;
	SET 局部变量名:=值;
	SELECT 局部变量名:=值;
#方式二：
	SELECT 字段 INTO 局部变量名
	FROM 表;
	
【使用（查看变量的值）】
SELECT 局部变量名;
```

# 九、存储过程和函数
* 类似于java中的方法
* 好处：<br>
1、提高代码的重用性<br>
2、简化操作<br>

## 9.1 存储过程
* 一组预先编译好的SQL语句的集合，理解成批处理语句<br>
1、提高代码的重用性<br>
2、简化操作
3、减少了编译次数并且减少了和数据库服务器的连接次数，提高了效率<br>

### 9.1.1 创建语法

```sql
CREATE PROCEDURE 存储过程名(参数列表)
BEGIN

	存储过程体（一组合法的SQL语句）
END

/*
1、参数列表包含三部分
参数模式  参数名  参数类型
举例：
in stuname varchar(20)

参数模式：
in：该参数可以作为输入，也就是该参数需要调用方传入值
out：该参数可以作为输出，也就是该参数可以作为返回值
inout：该参数既可以作为输入又可以作为输出，也就是该参数既需要传入值，又可以返回值

2、如果存储过程体仅仅只有一句话，begin end可以省略
存储过程体中的每条sql语句的结尾要求必须加分号。
存储过程的结尾可以使用 delimiter 重新设置
语法：
delimiter 结束标记
案例：
delimiter $
*/
```

### 9.1.2 调用
* CALL 存储过程名(实参列表);
### 9.1.3 查看
SHOW CREATE PROCEDURE  myp2;
### 9.1.4 删除
* 语法：drop procedure 存储过程名<br>
DROP PROCEDURE p1;<br>
### 9.15 示例

```sql
【空参列表】
【插入到admin表中五条记录】
DELIMITER $
CREATE PROCEDURE myp1()
BEGIN
	INSERT INTO admin(username,`password`) 
	VALUES('john1','0000'),('lily','0000'),('rose','0000'),('jack','0000'),('tom','0000');
END $

#调用
CALL myp1() $

【创建带in模式参数的存储过程】
【创建存储过程实现 根据女神名，查询对应的男神信息】
CREATE PROCEDURE myp2(IN beautyName VARCHAR(20))
BEGIN
	SELECT bo.*
	FROM boys bo
	RIGHT JOIN beauty b ON bo.id = b.boyfriend_id
	WHERE b.name=beautyName;
	

END $

#调用
CALL myp2('柳岩')$

【创建out 模式参数的存储过程】
【根据输入的女神名，返回对应的男神名】
CREATE PROCEDURE myp6(IN beautyName VARCHAR(20),OUT boyName VARCHAR(20))
BEGIN
	SELECT bo.boyname INTO boyname
	FROM boys bo
	RIGHT JOIN
	beauty b ON b.boyfriend_id = bo.id
	WHERE b.name=beautyName ;
	
END $

#调用

CALL myp6('小昭'，@bName)$
SELECT @bName$

【创建带inout模式参数的存储过程】
【传入a和b两个值，最终a和b都翻倍并返回】
CREATE PROCEDURE myp8(INOUT a INT ,INOUT b INT)
BEGIN
	SET a=a*2;
	SET b=b*2;
END $

#调用
SET @m=10$
SET @n=20$
CALL myp8(@m,@n)$
SELECT @m,@n$
```

## 9.2 函数
### 9.2.1 定义
* 一组预先编译好的SQL语句的集合，理解成批处理语句<br>
1、提高代码的重用性<br>
2、简化操作<br>
3、减少了编译次数并且减少了和数据库服务器的连接次数，提高了效率<br>

* 区别：<br>
存储过程：可以有0个返回，也可以有多个返回，适合做批量插入、批量更新<br>
函数：有且仅有1 个返回，适合做处理数据后返回一个结果<br>

### 9.2.2 创建语法

```sql
CREATE FUNCTION 函数名(参数列表) RETURNS 返回类型
BEGIN
	函数体
END
/*

注意：
1.参数列表 包含两部分：
参数名 参数类型

2.函数体：肯定会有return语句，如果没有会报错
如果return语句没有放在函数体的最后也不报错，但不建议

3.函数体中仅有一句话，则可以省略begin end
4.使用 delimiter语句设置结束标记

*/
```

### 9.2.3 调用语法
* SELECT 函数名(参数列表)

### 9.2.4 示例

```sql
【无参有返回】
【返回公司的员工个数】
CREATE FUNCTION myf1() RETURNS INT
BEGIN

	DECLARE c INT DEFAULT 0;#定义局部变量
	SELECT COUNT(*) INTO c#赋值
	FROM employees;
	RETURN c;
	
END $

SELECT myf1()$

【有参有返回】
【根据员工名，返回它的工资】
CREATE FUNCTION myf2(empName VARCHAR(20)) RETURNS DOUBLE
BEGIN
	SET @sal=0;#定义用户变量 
	SELECT salary INTO @sal   #赋值
	FROM employees
	WHERE last_name = empName;
	
	RETURN @sal;
END $

SELECT myf2('k_ing') $
```

### 9.2.5 查看函数&删除函数
* SHOW CREATE FUNCTION myf3;
* DROP FUNCTION myf3;

# 十、流程控制结构 
## 10.1 分支
* if(条件，值1，值2)
* case 表达式或字段<br>
when 值1 then 语句1;<br>
when 值2 then 语句2；<br>
## 10.2 循环

* loop 一般用于实现简单的死循环
* while 先判断后执行
* repeat 先执行后判断，无条件至少执行一次

































