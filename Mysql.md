# DBMS（数据库管理系统）：

​	数据库的管理软件，科学有效的管理我们的数据。维护和获取数据

​	MySQL，本质为数据库管理系统

## MySQL：

​	MySQL是一个关系型数据库管理系统，最好的RDBMS应用软件之一。体积小、速度快、总体拥有成本低，且是开源的数据库软件

# 基础语法：

## 一、启动关闭服务器：

​	net stop 服务名称;

​	net start 服务名称；

## 2、登录mysql：

使用bin目录下的命令进行连接

​	本地登录：

​		

```sql
mysql -uroot -p;

--输入密码
```

### 3、常用命令(不区分大小写）：

​	①查看数据库：

​		show databases;

​	②选择使用数据库：

​		use 数据库名字;

​	③创建数据库：

​		create database 名称;

### 4、数据库基本单位：

​	表(table)：

​	数据库中以表格形式表示数据。

​	在java中，数据库的一行往往使用一个对象表示





```sql
create database westos;  --创建一个数据库
exit;  --退出连接
--  表示sql语言的单行注释
/*
表示sql的多行注释
*/
```

# 二、操作数据库：

## 2.1操作数据库：（了解）

​	操作数据库 > 操作数据库中的表 > 操作表中的数据

==mysql关键字不区分大小写==

1、创建数据库

```sql
	CREATE DATABASE	[IF NOT EXISTS] westos;
```

2、删除数据库

```sql
	DROP DATABASE IF EXISTS hello;
```

3、使用数据库

```sql
-- tab键上面的，若名字或表明出现关键字时使用
SELECT `user` FROM student;
```

4、查看数据库

```sql
SHOW DATABASES; -- 查看所有的数据库
```

## 2.2数据类的列类型：

>数值：

​	![image-20211210162250288](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211210162250288.png)

![image-20211210162437224](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211210162437224.png)

![image-20211210162602637](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211210162602637.png)

## 2.3、数据库字段属性（重点）：

==Unsigned:==

​	1)无符号的整数

​	2）声明了该列不能声明为负数

==zerofill：==

​	1）0填充的

​	2）不足的位数，使用0来填充，int(3),  5 ---005

==自增：==

​	1）通常理解为自增，自动在上一条记录的基础上 + 1（默认为1，可以修改）

​	2）通常用来设计唯一的主键 ~index

==非空：==NULL not null

​	1）假设设置为nut null ，如果不给他赋值，就会报错

​	2）NULL ，如果不填写值，默认就是null

==默认：==

​	1）设置默认的值

​	2）如果不指定该列的值，则会有默认的值

## 2.4、创建数据库中的表：

```sql
-- AUTO_INCREMENT 自增
-- 字符串使用时需要使用单引号''括起来
-- DEFAULT  默认的
-- PRIMARY KEY 主键   为保证规范，全部写在最后，一般情况下一个表只有一个主键
-- ENGINE = INNODB  引擎使用的是INNODB
-- DATETIME 最大长度为6

CREATE TABLE `student`(
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
	`pwd` VARCHAR(30) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(2) NOT NULL DEFAULT '男' COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
	`email` VARCHAR(30) DEFAULT NULL COMMENT '电子邮件',
	PRIMARY KEY(`id`)
)ENGINE = INNODB DEFAULT CHARSET = utf8
```

### 格式：（背下来）

```sql
CREAT TABLE [IF NOT EXISTS] `表名`(
	`字段名` 列类型(长度) [属性] [索引] [注释],
    `字段名` 列类型(长度) [属性] [索引] [注释],
    ....
    `字段名` 列类型(长度) [属性] [索引] [注释],
)[表引擎] [字符集设置] [注释]
```

常用命令：

```sql
SHOW CREATE DATABASE school -- 查看数据库创建语言

SHOW CREATE TABLE `student` -- 查看表创建语言

DESC student -- 查看表的结构
```

## 2.5、数据表类型：

![image-20211210212805444](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211210212805444.png)

常规使用操作：

​	1）MYISAM : 节约空间速度较快

​	2）INNODB： 安全性较高，事物的处理，多表多用户操作

>在物理空间存放的位置

​	所有数据库文件都存在data目录下

​	本质还是文件的存储

> 设置数据库表的字符集编码

```sql
CHARSET = utf8
```

不设置的话，会是MySQL默认的字符集编码  （不支持中文）

## 2.6、修改删除表：

> 修改

```sql
-- 修改表明  ALTER TABLE 旧表名 RANAME AS 新表名    
ALTER TABLE students RENAME AS student1

-- 增加表的字段		ALTER TABLE 表名 ADD 字段名 列属性
ALTER TABLE student1 ADD age INT(11)

-- 修改表的字段 modify(修改)（重命名，修改约束）
ALTER TABLE student1 MODIFY age VARCHAR(11)  -- 修改约束	ALTER TABLE 表名 MODIFY 字段名 列属性[]
ALTER TABLE student1 CHANGE age age1 INT(1)  -- 修改字段重命名	ALTER TABLE 表名 CHANGE 旧名字 新名字 列属性[]

-- 修改表的字段 	ALTER TABLE 表名 DROP 字段名
ALTER TABLE student1 DROP age1 -- 删除字段名
```

> 删除

```sql
-- 删除表 ( 如果表存在，则进行删除操作 )
-- DROP TABLE IF EXISTS 表名
DROP TABLE IF EXISTS student1
```

==所有的创建和删除操作尽量加上判断，以免报错==

注意：

​	1）``  字段名，使用这个符号进行包裹  避免重复关键字

​	2）注释：  --     /**/

​	3）所有的符号都是英文状态

## 3、MySQL数据管理：

### 3.1外键：（了解）

```sql
CREATE TABLE `grade`(
	`gradeid` INT(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
	`gradename` VARCHAR(10) NOT NULL DEFAULT '匿名' COMMENT '年级名称',
	PRIMARY KEY(`gradeid`)
)

CREATE TABLE `student`(
	`id` INT(10) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(20) NOT NULL DEFAULT '匿名' COMMENT '姓名',
	`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
	`gradeid` INT(10) NOT NULL COMMENT '学生的年级id',
	`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭地址',
	`email` VARCHAR(20) DEFAULT NULL COMMENT '电子邮件',
	`date` DATETIME DEFAULT NULL COMMENT '出生日期',
	PRIMARY KEY(`id`)
)
-- 创建表的时候没有外键关系  reference  引用
ALTER TABLE `student` 
ADD CONSTRAINT `FK_gradeid` FOREIGN KEY(`gradeid`) REFERENCES `grade`(`gradeid`);
-- ALTER TABLE 表 ADD CONSTRAINT 约束名 FOREIGN KEY(`作为外键的列`) REFERENCES 那个表(哪个字段)
```

以上操作都是物理外键，数据库级别外键，不建议使用（避免数据库过多造成数据）

> 最佳：

​	数据库就是单纯的表，只用来存取数据，只有行（数据）和列（字段）

​	实用程序去实现外键	

删除有外键关系的表时，必须要先删除创建外键的表，再能删除引用

### 3.2🔺DML语言（核心为增删改查）（数据库管理语言）： 	

​	意义：数据存储，数据管理

- insert

  ```sql
  -- 插入语句 insert（添加）
  -- insert into 表名([字段名1],字段2，字段3） values('值1'),('值2'),('值3'),(...)
  INSERT INTO `grade`(gradename) VALUES('大一')
  
  -- 由于主键自增我们可以省略（如果不写表的字段，那么将会一一匹配，产生错误）
  INSERT INTO `grade` VALUES('大二')  -- 报错
  -- 写插入语句时，数据和字段一定要一一对应
  
  -- 插入多个字段
  INSERT INTO `grade`(gradename) VALUES('大二'),('大三'),('大四')
  ```

  语法：insert into 表名([字段名1],字段2，字段3） values('值1'),('值2'),('值3'),(...)

  注意事项：

  - 字段和字段之间使用英文逗号隔开
  - 字段是可以省略的，但是后面的值必须一一对应，不能少
  - 可以同时插入多条语句，VAKUES 后面的值，需要用 , 隔开 (),()

- update（修改）

  ```sql
  -- 修改信息  update
  UPDATE `student` SET `name` = '我自己' WHERE `id` = 1;
  
  -- 在不指定的情况下，列里的所有信息都会被修改
  UPDATE `student` SET `name` = '长江七号';
  
  -- 修改多个属性时，使用逗号隔开
  UPDATE 	`student` SET `name`= '我自己',`pwd` = '5555',`email` = '123546@qq.com' WHERE `id` = 1;
  -- 语法		colnum_name 为列名  value 为想修改成的结果
  -- update 表名 set colnum_name = value [,colnum_name = value....] where [条件]
  ```

  条件：where子句 运算符 id 等于某个值，大于某个值。。。

  ![image-20211211155035350](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211211155035350.png)

  注意：

  - colnum_name 是数据库的列，尽量带上``
  - 条件，筛选的条件，，如果没有指定，则会修改所有的列
  - value，是一个具体的值，也可以是一个变量
  - 多个设置的属性之间使用英文逗号隔开

- > delete（删除）：

   语法：==delete from 表名 [where 条件]==

```sql
-- 删除数据 (避免这样写，会删除整个表的数据）
DELETE FROM `student`

-- 删除了 id = 1 的数据
DELETE FROM `student` WHERE `id` = 1;
```

> TRUNCATE命令

作用：清空一个数据库表，表的结构和索引约束不会改变

```sql
-- 清空 student表
TRUNCATE `student`
```

> delete 与 TRUNCATE 区别

- 相同点：都能删除数据，不会删除表的结构
- 不同：
  - delete 删除表数据不会影响自增
  - TRUNCATE 重新设置 自增列 计数器回归零
  - TRUNCATE 不会影响事务

### 4、🔺DQL查询数据：

#### 4.1、DQL：

数据查询语言：

- 所有的查询操作均属用  Select
- 简单的查询、复杂的查询都能使用
- ==数据库中最核心的语言，最重要的语句==
- 使用频率最高的语言

#### 4.2、查询：

```sql
-- 查询全部学生  SELECT 字段 FROM 表
SELECT * FROM student

-- 查询指定字段
SELCET `student`,`StudentName` FROM student

-- 别名 给结果取一个名字   AS
SELECT `StudentNo` AS 学号,`StudentName` AS 学生姓名 FROM student 

-- 函数  Concat(a,b)
SELECT CONSAT('姓名：',StudentName) AS 新名字 FROM student
```

> 去重：（distinct）

```SQL
-- 去重   去除SELECT查询出来的结果中的重复的数据
SELECT DISTINCT `StudentNo` FROM result

-- 查询系统版本
SELECT VERSION()  --查询系统版本	

SELECT 100*3-1 AS 计算结果 -- 计算结果
```

#### 4.3、where条件语句：

作用：检索数据中符合条件的语句

```sql
SELECT studentNo,`StudentResult` FROM result
WHERE StudentResult BETWEEN 95 AND 100;   --  查询StudentResult在95-100之间的

-- 与   &&    and
-- 或   ||    or
-- 非   ！    not
```

> 模糊查询：比较运算符

![image-20211213102915428](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213102915428.png)**like的作用类似包含**

```sql
-- 查询姓刘的同学
-- like结合  %(代表0到任意一个字符)、    _(一个字符)
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘%'

-- 查询姓刘的同学，名字后面只有一个字
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘_'

-- 查询姓刘的同学，名字后面只有2个字
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘__'

-- 查询名字中有嘉字的同学，  %嘉%
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '%嘉%'

--   ====  in ====
--查询1001、1002、1003号的学生
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentNo IN(1001,1002,1003);

-- 查询在北京的学生
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `Address` IN('北京');

-- 查询地址为空的学生
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE address = '' OR address IS NULL;

--查询有出生日期的同学  不为空
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `BornDate` IS NOT NULL;
-- 为空
WHERE `BornDate` IS NULL;
```

#### 4.4、连表查询：

> join (连接的表) on (判断的条件)  连接查询  
>
> where 等值查询

![image-20211213141501212](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213141501212.png)

> 自连接：

==自己的表和自己的表连接，核心：一张表拆为两张一样的表==

![image-20211213144025802](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213144025802.png)

#### 4.5、分页和排序：

> 排序：order by

升序：ASC    降序：DESC

```sql
SELECT.....
.
.
.
WHERE...
ORDER BY StudentResult DESC   -- 根据StudentResult按照降序排列
```

> 分页：

缓解数据库压力。

```sql
-- 分页：每页只显示5条数据
-- 语法：    limit  起始值，页面大小

SELECT.....
.
.
.
WHERE...
ORDER BY StudentResult DESC   -- 根据StudentResult按照降序排列
LIMIT 1,5

-- 第一页  limit 0，5
-- 第二页  limit 5，5
-- 第三页  limit 10，5
```

#### 4.6、子查询：

本质：==在where语句中在嵌套一个查询语句==  由里即外

### 5.函数：

#### 5.1：常用函数：

数学运算：

```sql
SELECT ABS(-8)  	-- 绝对值
SELECT CEILING(9,4)	-- 向上取整
SELECT FLOOR(9,4)	-- 向下取整
SELECT RAND() 		-- 返回一个0-10的随机数

--  字符串函数
SELECT CHAR_LENGTH('即使在校的饭')  	-- 字符串长度
SELECT CONCAT('WO ','AI ')			-- 拼接字符串
SELECT INSERT('我爱编程'，1,2,'超级热爱')	-- 替换方式  1 开始的位置 2长度

```

#### 5.2、聚合函数（常用）：

![image-20211213153316756](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213153316756.png)

```sql
-- 统计表中的数据
SELECT COUNT(studentname) FROM student; 	-- Count(指定列)  （会忽略所有的null值）
SELECT COUNT(*) FROM student;				--Count(*)   (不会忽略null值)
SELECT COUNT(1) FROM student;				--Count(1)   (不会忽略所有的null值  本质是计算行数)
```

#### 5.3、数据库级别的MD5加密（扩展）：

MD5不可逆，具体的值的md5一样

![image-20211213154729139](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213154729139.png)

### 6、事务

### 6.1什么是事务：

==要么都成功，要么都失败==

将一组SQL放在一个批次中执行

> 事务原则：ACID原则  原子性，一致性，隔离性，持久性

原子性：![image-20211213163125721](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213163125721.png)

一致性：

![image-20211213163213169](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213163213169.png)



持久性：![image-20211213163330519](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213163330519.png)

事务一旦提交就不可逆

隔离性：![image-20211213163356241](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211213163356241.png)

多个事务同时进行不会相互影响

```sql
-- mysql是默认开启事务自动提交的
SET autocommit = 0 /* 关闭*/
SET autocommit = 1 /* 开启（默认的）*/

-- 手动处理事务
SET autocommit = 0 -- 关闭自动提交
-- 事务开启
START TRANSACTION  -- 标记一个事务的开始，之后的sql都在一个事务中

INSERT XX
INSERT XX

--体骄傲：持久化（成功！）
COMMIT
--回滚：回到原来的样子（失败）
ROLLBACK

-- 事务结束
SET autocommit = 1 -- 开启自动提交

-- 了解
SAVEPOINT 保存点名  -- 设置一个事务的保存点
ROLLBACK TO SAVEPOINT 保存点名  -- 回滚到保存点
RELEASE SAVEPOINT 保存点名  -- 撤销保存点
```

![image-20211214092307486](C:/Users/10606/AppData/Roaming/Typora/typora-user-images/image-20211214092307486.png)



> 模拟事务：

```sql
CREATE DATABASE IF NOT EXISTS shop
USE shop

CREATE TABLE `account`(
	`id` INT(4) NOT NULL AUTO_INCREMENT,
	`name` VARCHAR(10) NOT NULL,
	`money` DECIMAL(9,2) NOT NULL, 
	PRIMARY KEY(`id`)
)

INSERT INTO account(`name`,`money`)
VALUES ('a',20000),('b',1000)

-- 模拟事务转账
SET autocommit = 0  -- 关闭自动提交
START TRANSACTION   -- 开启一个事务
UPDATE account SET money = money - 500 WHERE `name` = 'a'  -- a 减500
UPDATE account SET money = money + 500 WHERE `name` = 'b' 

COMMIT;   --  提交事务，就会被持久化
ROLLBACK;  -- 回滚
SET autocommit = 1; -- 恢复默认值
```

### 7、索引：

> 帮助MySQL高效获取数据的数据结构
>
> 索引时数据结构

#### 7.1、索引的分类：

- 主键索引（PRIMARY KEY)
  - 唯一标识，主键不能重复，只能有一个列为主键
- 唯一索引（UNIQUE KEY）
  - 避免重复的列出现，唯一索引可以重复，多个列都可以标识为唯一索引
- 常规索引（KEY/INDEX）
  - 默认的，index key关键字
- 全文索引（FullText）
  - 在特定的数据库引擎下才有
  - 快速定位数据

基础语法

```sql
-- 显示所有的索引信息
SHOW INDEX FROM student
-- 增加一个全文索引  （索引名） 列名
ALTER TABLE school.student ADD FULLTEXT INDEX `studentName`(`studentName`);

-- EXPLAIN 分析sql执行的状况
EXPLAIN SELECT * FROM student; -- 非全文索引

EXPLAIN SELECT * FROM student WHERE MATCH(studentName) AGAINST('刘') -- 姓刘的同学
```



#### 7.2、索引原则：

- 索引不是越多越好
- 不要对进程变动数据加索引
- 小数据量的表不需要加索引
- 索引一般加在常用来查询的字段上

### 8、数据库管理与备份：

#### 8.1、用户管理：

![image-20211214133356844](../java%E8%BD%AF%E4%BB%B6/TyporaPhoto/image-20211214133356844.png)



> SQL命令：

用户表：mysql.user

```sql
-- 创建用户 CREAT USER 用户名 IDENTIFIED BY '密码'
CREATE USER ZHOUBO IDENTIFIED BY '123456'

-- 修改密码  （修改当前用户密码）
SET PASSWORD = PASSWORD('111111')

-- 修改密码  （修改指定用户密码）
SET PASSWORD FOR ZHOUBO = PASSWORD('123456')

-- 给用户进行重命名    RENAME USER 原来的名字 TO 新的名字
RENAME USER zhoubo TO zhoubo1

-- 用户授权   ALL PRIVILEGES 全部的授权， 库.表
-- 除了给别人授权   其他所有事都可以干
GRANT ALL PRIVILEGES ON *.* TO zhoubo2    -- 将所有库以及所有表的权限给zhoubo2

-- 查看权限
SHOW GRANTS FOR zhoubo2  -- 查看指定用户权限

-- 撤销权限  REMOVE 哪些权限  在哪个库  给谁撤销
REMOVE ALL PRIVILEGES ON *.* FROM zhoubo2

-- 删除用户
DROP USER zhoubo2   -- 删除用户  zhoubo2
```

#### 8.2、数据库备份：

- 保证重要数据不丢失
- 数据转移

备份方式：

- 直接拷贝物理文件
- 在Sqlyog这种可视化工具中进行手工导出
  - 在想要导出的表或者库中右键导出
  - ![image-20211214140816309](../java%E8%BD%AF%E4%BB%B6/TyporaPhoto/image-20211214140816309.png)
- 使用命令行导出 mysqldump 命令行导出

```sql
-- mysqldump -h 主机 -u 用户名 -p 密码 数据库  表1[ 表2，表3....]  > 物理磁盘位置/文件名
mysqldump -hlocalhost -uroot -p12356 school student >D:/a.sql

-- 导入表   先登陆数据库，使用相应的库  再使用source方法
source d:/a.sql；
```

### 9、数据库设计：

#### 9.1、设计：

==当数据库较为复杂时，使用设计==

##### 糟糕的数据库设计：

- 数据冗余，浪费空间
- 数据库插入和删除都会麻烦、异常【屏蔽使用】



##### 良好的数据库设计：

- 节省内存空间
- 保证数据库的完整性

##### 软件开发中的数据库设计：

- 分析需求：分析业务和需要处理的数据库需求
- 概要设计：设计关系图E-R图

##### 设计数据库步骤：（个人博客）

- 收集信息，分析需求
  - 用户表（用户登录注销，用户个人信息，写博客，创建分类）
  - 分表类（文章分类，谁创建的）
  - 文章表（文章的信息）
  - 评论表
  - 友链表（友链信息）
  - 自定义表（系统信息，某个关键的字，或者一些主字段）
- 标识实体（把需求落地到每个字段）
- 标识实体 之间的关系
  - 写博客：user -- > blog
  - 创建分类：user -- >category
  - 关注：user -- >user
  - 友链：links
  - 评论：user - user- blog

#### 9.2、三大范式：

**为什么要数据库规范？**

- 信息重复
- 更新异常
- 插入异常
  - 无法正常显示信息
- 删除异常
  - 丢失有效信息

> 三大范式

**第一范式（1NF）**

原子性：保证每一列不可再分

**第二范式（2NF）**

前提：满足第一范式

每张表只描述一件事情

![image-20211214144634979](../java%E8%BD%AF%E4%BB%B6/TyporaPhoto/image-20211214144634979.png)

**第三范式（3NF）**

前提：满足第一范式和第二范式

需要确保表中的每一列数据都和主键直接相关，而不能间接相关

![image-20211214144743823](../java%E8%BD%AF%E4%BB%B6/TyporaPhoto/image-20211214144743823.png)



**规范性 和 性能的问题**

关联查询的表不能超过三张表

- 考虑商业化的需求和目标（成本，用户体验）  数据库的性能更加重要
- 在规范性能的问题的时候，需要适当的考虑一下规范性
- 故意给某些表增加一些冗余的字段（从多表查询中变为单表查询）
- 故意增加一些计算列（从大数据查询将为小数据查询：索引）

## 10、JDBC（重点）

### 10.1、数据库驱动

![image-20211214145332158](../java%E8%BD%AF%E4%BB%B6/TyporaPhoto/image-20211214145332158.png)

程序会通过数据库 驱动 与数据库打交道

### 10.2、JDBC

sun公司为了简化开发人员对（数据库的同意）操作，提供了一个（Java操作数据库的）规范，俗称JDBC   只需要掌握JDBC接口操作

![image-20211214150635168](../java%E8%BD%AF%E4%BB%B6/TyporaPhoto/image-20211214150635168.png)

### 10.3、第一个JDBC程序：

> 创建测试数据库

```sql
CREATE DATABASE `jdbcStudy` CHARACTER SET utf8 COLLATE utf8_general_ci;

USE `jdbcStudy`;

CREATE TABLE `users`(
 `id` INT PRIMARY KEY,
 `NAME` VARCHAR(40),
 `PASSWORD` VARCHAR(40),
 `email` VARCHAR(60),
 birthday DATE
);

 INSERT INTO `users`(`id`,`NAME`,`PASSWORD`,`email`,`birthday`)
VALUES('1','zhangsan','123456','zs@sina.com','1980-12-04'),
('2','lisi','123456','lisi@sina.com','1981-12-04'),
('3','wangwu','123456','wangwu@sina.com','1979-12-04')
```

![image-20211214155143218](../java%E8%BD%AF%E4%BB%B6/TyporaPhoto/image-20211214155143218.png)
