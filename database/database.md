# DateBase

## 三层模式
- 物理模式 
- 逻辑模式
- 视图模式/子模式

## 数据库中的DDL和DML

在数据库管理中，DDL（Data Definition Language，数据定义语言）和DML（Data Manipulation Language，数据操作语言）是两种常见的SQL（结构化查询语言）语句类型，用于不同的目的。

### DDL（Data Definition Language 数据定义语言）
DDL用于定义或修改数据库结构的语句集。主要包括：

- **CREATE**：创建新的数据库对象，如表格（CREATE TABLE）、索引（CREATE INDEX）等。
- **ALTER**：修改现有数据库对象的结构，比如添加、修改或删除表中的列。
- **DROP**：删除数据库中的对象。
- **TRUNCATE**：删除表中的所有行，但不删除表本身。

DDL操作通常会影响数据库的元数据，并且这些操作往往是不可逆的。

### DML（Data Manipulation Language 数据操作语言）
DML主要用于添加、修改、查询或删除数据库中的数据。包括：

- **SELECT**：查询数据库中的数据。这是最常用的DML命令。
- **INSERT**：向表中添加新行。
- **UPDATE**：修改表中的现有数据。
- **DELETE**：从表中删除行。

DML操作直接影响表中的数据，但不改变表的结构。通常，这些命令可以被撤销（除非在不支持事务的数据库系统中执行）。

## SQL具体使用
### Select
#### 基本使用
SELECT column1, column2 FROM table_name;
这里，column1 和 column2 是你想从 table_name 表中选择的列名。
#### 使用 * 选择所有列
SELECT * FROM table_name;
#### 使用 WHERE 子句
SELECT column1, column2 FROM table_name WHERE condition;
#### 使用 ORDER BY 排序
SELECT column1, column2 FROM table_name ORDER BY column1 [ASC|DESC];
*默认情况下，排序是升序（ASC），但你也可以指定降序（DESC）。*
#### 聚合函数
*SQL 提供了多种聚合函数，如 COUNT(), SUM(), MAX(), MIN(), AVG() 等，这些可以用在 SELECT 语句中来计算或汇总数据：*
SELECT COUNT(column1), AVG(column2) FROM table_name WHERE condition;
#### JOIN 多个表
*SELECT 语句可以结合 JOIN 来从多个表中选择并结合数据：*
SELECT table1.column1, table2.column2
FROM table1
JOIN table2 ON table1.common_column = table2.common_column;

### Insert
#### 基本使用
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
*这里，table_name 是你要插入数据的表名，column1 和 column2 是要插入的列名，value1 和 value2 是要插入的值。*

#### 批量插入
INSERT INTO table_name (column1, column2)
VALUES (value1, value2),
    (value3, value4),
    (value5, value6);
*这里，table_name 是你要插入数据的表名，column1 和 column2 是要插入的列名，value1、value2、value3、value4、value5、value6 是要插入的值。*

### Update
#### 基本使用
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
*这里，table_name 是你要更新数据的表名，column1 和 column2 是要更新的列名，value1 和 value2 是要更新的值，condition 是更新的条件。*
#### 更新多个列
UPDATE table_name SET column1 = value1, column2 = value2, column3 = value3 WHERE condition;
*同时更新多个列的值。*


### Delete
#### 基本使用
DELETE FROM table_name WHERE condition;
*这里，table_name 是你要删除数据的表名，condition 是删除的条件。*
#### 删除所有行
*DELETE FROM table_name;*

### Group By
#### 基本使用
SELECT column1, COUNT(column2) FROM table_name GROUP BY column1;
*这里，column1 是你要分组的列名，column2 是你要计数的列名，table_name 是你要查询的表名。*

### Having
#### 基本使用
SELECT column1, COUNT(column2) FROM table_name GROUP BY column1 HAVING COUNT(column2) > 10;
*这里，column1 是你要查询的列名，column2 是你要计数的列名，table_name 是你要查询的表名，COUNT(column2) > 10 是你要过滤的条件。*

### Union
#### 基本使用
SELECT column1 FROM table1
UNION
SELECT column1 FROM table2;
*这里，column1 是你要查询的列名，table1 和 table2 是你要查询的表名*

### Order By
#### 多列排序
SELECT column1, column2 FROM table_name ORDER BY column1 ASC, column2 DESC;
*这里，column1 和 column2 是你要排序的列名，table_name 是你要查询的表名。默认情况下，column1 是升序排序，column2 是降序排序。*

### Limit
#### 基本使用
SELECT column1 FROM table_name LIMIT 10;
*这里，column1 是你要查询的列名，table_name 是你要查询的表名，10 是你要限制的行数。*

## 数据库存储管理核心概念

### 存储管理器
存储管理器是数据库管理系统的一个核心组件，负责管理物理存储介质，主要包括以下几个方面：

#### 1. 数据文件管理
管理数据库中的物理文件，这包括数据文件、索引文件和元数据文件等。
- **数据文件**：存储实际数据的文件。
- **索引文件**：存储索引信息，帮助快速检索数据。

#### 2. 缓存管理
缓存管理主要负责数据在内存中的缓存，以减少对磁盘的直接访问，提高数据访问速度。
- **数据预加载**：根据访问模式预测并加载常用数据到缓存。
- **替换策略**：如LRU（最近最少使用）、FIFO（先进先出）策略，管理内存中的数据。

#### 3. 事务和并发控制
负责维持事务的ACID属性，并管理并发访问，确保数据的一致性和完整性。
- **事务日志**：记录所有事务操作，以支持事务的持久性和恢复。
- **锁机制**：防止数据访问冲突，支持多用户环境下的数据一致性。

#### 4. 备份与恢复
系统的备份与恢复机制确保数据的持久安全，防止数据丢失。
- **定期备份**：定期对数据库数据进行备份。
- **恢复策略**：在数据丢失或损坏时恢复数据。

#### 5. 数据分区与分片
通过数据分区和分片提高大规模数据库系统的性能和扩展性。
- **数据分区**：将数据分布在不同的存储区域。
- **分片**：根据特定规则将数据分布到多个服务器。

这些管理功能共同工作，保证数据库系统的高性能、高可用性和扩展性。

