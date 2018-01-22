# mysql使用记录

## 启动mysql服务器

`mysqld start`

## 登录

```
mysql -h主机地址 –user=root –password=123456 db_name;
mysql –u root –p123456 db_name;
```

## 修改用户密码

`mysqladmin -u root -p ab12 password djg345`

## 权限管理

### 添加用户

`create user username1 identified by ‘password’ , username2 identified by ‘password’;`

### 授权

`grant select, insert, update, delete, create,drop on fangchandb.* to custom@ it363.com identified by passwd;`

`grant all privileges on *.* to monty@localhost identified by ’something’ with grant option;`

`grant all on db_name.table_name to user_name [ indentified by ‘password’ ];`

### 删除授权

```
revoke all privileges on *.* from root@”%”;
delete from user where user=”root” and host=”%”;
```

### 更新用户权限

`flush privileges;`

## 数据库管理

`show databases;` 显示所有数据库

`use databasename;` 选择数据库

`create database if not exists name;` 创建数据库

`drop database if exists name;` 直接删除数据库，不提醒

## 表管理

`show tables;` 显示数据库mysql中所有的表

`desc tablename;` 表的详细描述

`create table mytable (id int , username char(20));` 创建数据表

`alter table users character set gbk;` 更改表的字符集

`alter table t1 rename t2;` 重命名表

`alter table table_name add column 字段名 字段类型 after 某字段；` 插入字段

`alter table table_name drop字段名;` 删除一个字段

`alter table table_name change 旧字段名 新字段名 新字段的类型;` 修改字段

`insert into mytable (id,username) values (1,’zhangsan’);` 插入表记录

`update mytable set username=’lisi’ where id=1;` 更新表记录

`delete from table_name where id=3;` 删除表记录

`drop table table_name;` 删除表数据

`truncate table table_name;` 清空表数据

`select id,username from mytable where id=1 order by desc;`

`select a.nickname,b.nickname from users a,users b where a.id>b.id ;`

`select id,nikename,address from users where id>(select id from users where nikename='lyh1');`

## 备份与恢复

```
mysqldump -h host -u root -p dbname > dbname_backup.sql；
mysqldump -h host -u root -p dbname < dbname_backup.sql；
```

## 导入导出数据

`load data local infile “mysql.txt” into table 表名;`

`mysqldump -u user_name -p database_name table_name > outfile_name.sql` 导出一个表

`mysqldump -u user_name -p -d –add-drop-table database_name > outfile_name.sql` 导出数据库结构

`mysqldump -uroot -p –default-character-set=latin1 –set-charset=gbk –skip-opt database_name > outfile_name.sql`

**导入.sql文件**

`use 数据库名;`

`source d:/mysql.sql;`

`mysql -uroot -p密码 < c://school.sql`

`mysql> source c://school.sql;`
