## 数据操作

* 查询
	* 查询所有数据库
		* SHOW DATABASES ;
	* 查询当前数据库
		* SELECT DATABASE();
* 创建
	* CREATE DATABASE [ IF NOT EXISTS] 数据库名 [ DEFAULT CHARSET 字符集 ] [ COLLATE 排序规则];
* 删除
	* DROP DATABASE [IF EXISTS] 数据库名;
* 使用
	* USE 数据库名;

## 表操作

* 查询
	* 查询当前数据库所有表
		* SHOW TABLES;
	* 查询表结构
		* DESC 表名;
	* 查询指定表的建表语句
		* SHOW CREATE TABLE 表名;
* 创建

```
CREATE TABLE表名(
	字段1 字段1类型[COMMENT 字段1注释]，
	字段2 字段2类型[COMMENT 字段2注释]，
	字段3 字段3类型[COMMENT 字段3注释]，
	......
	字段n 字段n类型[COMMENT 字段n注释]
)[COMMENT 表注释];
```

* 修改
	* 添加字段
		* ALTER TABLE 表名 ADD 字段名 类型 (长度) [COMMENT 注释 ] [约束];
	* 修改数据类型
		* ALTER TABLE 表名 MODIFY 字段名 新数据类型 (长度);
	* 修改字段名和字段类型
		* ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型 (长度) [COMMENT 注释] [约束];
	* 删除字段
		* ALTER TABLE 表名 DROP 字段名;

## 数据类型

### 数值类型

![[Pasted image 20230322144939.png]]

### 字符串类型

![[Pasted image 20230322145116.png]]

### 日期时间类型

![[Pasted image 20230322145343.png]]
