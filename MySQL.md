# MySQL

### DDL-数据库操作 

##### 查询

**大小写均可**

- 查询数据库:SHOW DATABASES;

- 查询当前数据库:SELECT DATABASE();

##### 创建

- CREATE DATABASE IF NOT EXISTS 数据库名;

##### 删除

- DROP DATABASE IF EXISTS 数据库名;

##### 使用

- USE 数据库名;

##### 查询当前数据库所有表

- SHOW TABLES;

##### 查询表结构

- DESC 表名;

##### 查询指定表的建表语句

- SHOW CREATE TABLE 表名;

##### 表操作-创建

```mysql
CREATE TABLE tb_user(id int comment '编号',name VARCHAR(50) COMMENT '姓名',
age int comment '年龄',gender VARCHAR(1) comment '性别')comment '用户表';
```

##### 添加字段

- ALTER TABLE 表名 ADD 字段名 类型(长度) COMMENT注释;

##### 修改数据类型

- ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);

##### 修改字段名和字段类型

- ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度);

#####  删除字段名

- ALTER TABLE 表名 DROP 字段名

## DML-数据库操作

全称是Data Manipulation Language(数据操作语言), 用来对数据库中表的数据记录进行增删改操作

##### 添加数据

1.给指定字段添加数据

- INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...);

2.给全部字段添加数据

- INSERT INTO 表名 VALUES(值1,值2,...);

3.批量添加数据

- INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...),(值1,值2,...);

- INSERT INTO 表名 VALUES(值1,值2,...),(值1,值2,...);

```mysql
INSERT INTO tb_user(id,name,age,gender) values(1,'七娃',18,'男');
INSERT INTO tb_user values(2,'六娃',19,'男'),(3,'花花',20,'女');
```

##### 修改数据

- UPDATE 表名 SET 字段名1=值1,字段名2=值2,...[WHERE 条件]

```mysql
UPDATE tb_user SET name='CC' WHERE sex='男'; //这个条件可以是任意一项
```

##### 删除数据

- DELETE FROM 表名 WHERE 条件;

## DQL-数据库操作

DQL全称是Data Query Language(数据查询语言),数据查询语言,用来查询数据库中表的记录

**关键字:SELECT**

##### DQL-基本查询

查询多个字段

- SELECT 字段1,字段2,字段3...FROM 表名;

```mysql
SELECT name,worknum,age from tb_user;
```

- SELECT *FROM 表名;

```mysql
SELECT *FROM tb_user; //全字段查询
```

##### DQL-条件查询

- SELECT 字段列表 FROM 表名 WHERE 条件列表;

```mysql
SELECT *FROM tb_user WHERE age!=18;//查询的是年龄不为18的所有员工信息
SELECT *FROM tb_user WHERE idcard is not null;//查询的是idcard不为null的员工信息
```

##### DQL-聚合函数

将一列数据作为一个整体,进行纵向计算

- SELECT 聚合函数(字段列表) FROM 表名;

```mysql
select count(age)from tb_user;//有年龄的员工数量
select avg(age)from tb_user;//所有员工年龄的平均值
select max(age)from tb_user;//员工中年龄最大的
select min(age)from tb_user;//年龄最小的
select sum(age) from tb_user where sex='男';//计算性别为男的员工的年龄总合
```

##### DQL-分组查询

- SELECT 字段列表 FROM 表名 [WHERE ] GROUP BY 分组字段名 [HAVING 分组后过滤条件];

- ```mysql
  select sex,count(sex) from tb_user where age=19 GROUP BY sex;//执行的是 以sex计数,年龄为19的人 按sex分组 有多少人 男 女分别多少 显示性别与人数
  select sex,avg(age) from tb_user GROUP BY sex;//以sex分组 计算各组的年龄平均值 显示年龄与人数
  select age,count(*) from tb_user where age<20 GROUP BY age HAVING count(*)>=2;//以age分组,计算年龄小于20 并且有两人以上是同一岁数的人 先试试年龄和人数
  ```

- **注意事项**

- 执行顺序:where>聚合函数>having

- 分组之后,查询的字段一般为聚合函数和分组字段,查询其他字段无任何意义

##### DQL-排序查询

- SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1,字段2 排序方式2;
- 排序方式:

- ASC:升序(默认值)
- DESC:降序 

```mysql
SELECT  *from tb_user ORDER BY age ASC;//根据年龄排升序 显示所有信息
SELECT *FROM tb_user ORDER BY entrydate DESC;//根据入职时间排降序 显示所有信息
SELECT *FROM tb_user ORDER BY age ASC,entrydate DESC;//先根据年龄排序 年龄一样的 根据入职时间排序 入职时间按降序排序
```

##### DQL-分页查询

- SELECT 字段列表 FROM 表名 LIMIT 起始索引,查询记录数;

- 起始索引从0开始,起始索引=(查询页码-1)*每页显示记录数

- ```mysql
  SELECT *FROM tb_user LIMIT 3,3;//查询第2页的三个数据 (2-1)*3=3
  ```

## 案例

```mysql
SELECT *FROM tb_user WHERE age=18||age=19;//查询 年龄为18.19岁的人
SELECT *FROM tb_user WHERE sex='男' GROUP BY name HAVING age>18;//查询 性别为男 小于十八岁的 按姓名分组
SELECT sex,count(sex) FROM tb_user WHERE age<20 GROUP BY sex;//查询年龄小于20岁的人 并且按性别分组 计算小于20岁的人男女各有多少人
SELECT name,age FROM tb_user WHERE age<20 ORDER BY age ASC,entrydate DESC;//查询 年龄小于二十岁的人并且排序 得到的值返回结果获取名字和年龄
SELECT *FROM tb_user WHERE sex='女'&&age<21 ORDER BY age ASC,entrydate DESC LIMIT 0,3;//查询 年龄小于21且性别为女的信息 按照年龄和入职时间排序 只展示前三项
```

## 案例-2

```mysql
CREATE TABLE sh_user_shopcart(
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT '购物车id',
user_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '用户id',
goods_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '商品id',
goods_price DECIMAL(10,2) UNSIGNED NOT NULL DEFAULT 0 COMMENT '单价',
goods_num INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '购买件数',
is_select TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否选中',
create_time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
update_time DATETIME DEFAULT NULL COMMENT '更新时间')ENGINE=InnoDB DEFAULT CHARSET=utf8;
CREATE TABLE sh_user_address(
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT '地址 id',
user_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '用户 id',
is_default TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否默认',
province VARCHAR(20) NOT NULL DEFAULT ''COMMENT '省',
city VARCHAR(20) NOT NULL DEFAULT '' COMMENT '市',
district VARCHAR(20) NOT NULL DEFAULT ''COMMENT '区',
address VARCHAR(255) NOT NULL DEFAULT ''COMMENT '具体地址',
zip VARCHAR(20) NOT NULL DEFAULT ''COMMENT '邮编',
consignee VARCHAR(20) NOT NULL DEFAULT ''COMMENT '收件人',
phone VARCHAR(20) NOT NULL DEFAULT ''COMMENT '联系电话',
create_time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
uodate_time DATETIME DEFAULT NULL COMMENT '更新时间'
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
CREATE TABLE sh_order(
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT '订单 id',
user_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '用户 id',
total_price DECIMAL(10,2) UNSIGNED NOT NULL DEFAULT 0 COMMENT '订单总价',
order_price DECIMAL(10,2) UNSIGNED NOT NULL DEFAULT 0 COMMENT '应付金额',
province VARCHAR(20) NOT NULL DEFAULT ''COMMENT '省',
city VARCHAR(20) NOT NULL DEFAULT '' COMMENT '市',
district VARCHAR(20) NOT NULL DEFAULT ''COMMENT '区',
address VARCHAR(255) NOT NULL DEFAULT ''COMMENT '具体地址',
zip VARCHAR(20) NOT NULL DEFAULT ''COMMENT '邮编',
consignee VARCHAR(20) NOT NULL DEFAULT ''COMMENT '收件人',
phone VARCHAR(20) NOT NULL DEFAULT ''COMMENT '联系电话',
is_valid TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否有效',
is_cancel TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否取消',
is_pay TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否付款',
status TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '物流信息',
is_del TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否删除',
create_time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
uodate_time DATETIME DEFAULT NULL COMMENT '更新时间'
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
CREATE TABLE sh_order_goods(
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT 'id',
order_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '订单 id',
goods_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '商品 id',
goods_name VARCHAR(120) NOT NULL DEFAULT '' COMMENT '商品名称',
goods_num INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '购买数量',
goods_price DECIMAL(10,2) UNSIGNED NOT NULL DEFAULT 0 COMMENT '单价',
user_not VARCHAR(255) NOT NULL DEFAULT '' COMMENT '用户备注',
staff_nota VARCHAR(255) NOT NULL DEFAULT '' COMMENT '卖家备注'
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
CREATE TABLE sh_goods_score(
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT COMMENT '评分 id',
user_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '用户id',
goods_id INT UNSIGNED NOT NULL DEFAULT 0 COMMENT '商品id',
goods_score TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '商品评分',
service_score TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '服务评分',
express_score TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '物流评分',
is_invalid TINYINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '是否无效',
create_time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '评分时间'
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

## 案例-3

```mysql
create database if not exists db;
use db;#使用数据库的名称
create table sh_student#创建表单
(
num int not NULL primary key comment '学号',
s_name char(8) comment'姓名',
sex char(2) comment'性别',
age  tinyint comment'年龄',
major char(16) comment'专业',
address char(50) comment'家庭住址'
)ENGINE=InnoDB DEFAULT CHARSET=utf8;   #这里一定是这样 如果只是CHARSET=utf8会报错
insert into sh_student(num,s_name,sex,age,major,address) values   #添加数据 到表名中 后面的括号不能省略 有点类似传参
(200809412,'庄小燕','女',24,'计算机','上海市中山北路12号'),
(200809415,'洪波','男',25,'计算机','青岛市解放路105号'),
(200109102,'肖辉','男',23,'计算机','杭州市凤起路111号'),
(200109103,'柳嫣红','女',22,'计算机','上海市邯郸路1066号'),
(200307121,'张正正','男',20,'应用数学','上海市延安路123号'),
(2000307122,'李丽','女',21,'应用数学','杭州市解放路56号');
select *from sh_student;   #选择表单展示所有内容
alter table sh_student add column datatime INT NOT NULL after address; #用add column语句 在address后面在增加一个数据名为datatime 
select *from sh_student;   #再次查看表单
alter table sh_student modify column age int; #修改age一栏的数据类型

use db;
create table curriculum(
CourseNum char(4) not NULL primary key comment'课程号',
CourseName char(20) comment'课程名',
StudyTime int comment'学时分',
Credit int comment'学分'
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

alter table curriculum add column achievement int default 0;
alter table curriculum modify column achievement  char(4);
alter table curriculum change achievement mark char(4) default 0;
alter table curriculum drop column mark;
drop table curriculum;#关闭
rename table db.sh_student to db.sh_Students;#改名
```

