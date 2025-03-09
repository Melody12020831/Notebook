---
statistics: True
comments: true
---

# SQL learning

!!! abstract
    推荐大家在 B站 看 GeekHour 的 SQL 速成课程，讲的很清楚。

    这里是我的学习笔记。

sql(**structured query language**) 是一种关系型数据库语言。

- 数据定义语言 `CREATE`、`DROP`、`ALTER`、`TRUNCATE`
- 数据操作语言 `INSERT`、`UPDATE`、`DELETE`、`CALL`
- 数据查询语言 `SELECT`
- 数据控制语言 `GRANT`、`REVOKE`

---

`MySQL` 中的数据类型大致可以分为五个大的类别。包括数值类型、日期和时间类型、字符串类型、json类型和空间类型。

- 数值类型分为**整数类型**和**浮点数类型**
    - 整数类型根据占用的存储空间的不同分为 `TINYINT`  `SMALLINT` 和 `BIGINT` 分别对应1-8个字节的存储空间，可以存储不同范围的整数。
    - 浮点数类型分为 `FLOAT` 和 `DOUBLE` 分别对应4个字节和8个字节的存储空间，可以存储不同范围的浮点数。

- 日期和时间类型包括 `DATE`、`TIME`、`DATETIME` 和 `TIMESTAMP` ,分别对应日期、时间、日期时间和时间戳。
- 字符串类型包括 `CHAR`、`VARCHAR`、`TEXT` 和 `BLOB` 等等，分别对应定长字符串、变长字符串、文本以及二进制数据。
- 比较新版的 MySQL 还支持 json 类型和点线空间等几何类型。

---

## 一些**基本操作**

- `DESC player;` 用于查看表的结构，`DESC` 是 `describe` 的缩写。
- `ALTER TABLE player MODIFY COLUMN name VARCHAR(200);` 用于修改表中的列。
- `ALTER TABLE player RENAME COLUMN name TO nick_name;` 用于修改列名。
- `ALTER TABLE player ADD COLUMN last_login DATETIME;` 用于添加列。
- `ALTER TABLE player DROP COLUMN last_login;` 用于删除列。
- `DROP TABLE player;` 用于删除表。

---

## **数据的增删查改**

`INSERT INTO player(id, name, level, exp, gold) VALUES(1, '张三', 1,1,1);` 用于插入数据。如果表名后面的括号中包括了所有的列，并且顺序也和表结构保持一致的话，那么这个括号以及它里面的列名就都可以省略掉，直接在表名后面加上 `VALUES` 关键字，然后加上要插入的数据即可。也可以写上部分列的名称，这样没有写出来的列会使用建表时设置的默认值。

`SELECT * FROM player;` 用于查询数据。`SELECT` 关键字后面可以跟一个星号，表示查询所有的列。也可以跟具体的列名，表示查询指定的列。

`INSERT INTO player(id, name) VALUES(2, '李四'),(3, '王五');` 用于插入多条数据。

`ALTER TABLE player MODIFY LEVEL INT DEFAULT 1;` 用于设置默认值。

`UPDATE player SET level = 1 WHERE name = '李四';` 用于更新数据。

`DELETE FROM player WHERE name = '李四';` 用于删除数据。

---

## 数据的导入导出

`mysqldump -u root -p game player > player.sql` 用于导出数据。`-u` 后面跟的是用户名，`-p` 后面跟的是密码，`game` 是数据库名，`player` 是表名，`player.sql` 是导出的文件名。表的名称可以省略，这样会导出整个数据库。

`mysql -u root -p game < player.sql` 用于导入数据。`-u` 后面跟的是用户名，`-p` 后面跟的是密码，`game` 是数据库名，`player.sql` 是导入的文件名。

---

## 常用语句

### `SELECT`

`SELECT * FROM player WHERE level > 1 AND level < 5;` 用于查询 level 大于 1 并且小于 5 的数据。

优先级顺序是 `()` > `NOT` > `AND` > `OR`。

---

### `IN`

可以用 `IN` 指定多个值。

`SELECT * FROM player WHERE level IN (1, 2, 3);` 用于查询 level 在 1、2、3 中的数据。

---

### `BETWEEN`

可以用 `BETWEEN` 和 `AND` 指定一个范围。

`SELECT * FROM player WHERE level BETWEEN 1 AND 3;` 用于查询 level 在 1 到 3 之间的数据。包括 1 和 3。

---

### `NOT`

可以用 `NOT` 取反。

`SELECT * FROM player WHERE level NOT BETWEEN 1 AND 3;` 用于查询 level 不在 1 到 3 之间的数据。

---

### `LIKE` and `REGEXP`

可以用 `LIKE` 模糊查询。

`SELECT * FROM player WHERE name LIKE '李%';` 用于查询 name 以 李 开头的数据。百分号表示任意字符，下划线表示任意一个字符。

!!! note "正则表达式中的常用通配符"
    - `.` 匹配任意单个字符
    - `^` 匹配字符串的开始
    - `$` 匹配字符串的结束
    - `[abc]` 匹配括号内的任意一个字符
    - `[a-z]` 范围内的任意一个字符
    - `A|B` 匹配 A 或 B

`SELECT * FROM player WHERE name REGEXP '^李.$';` 用于查询 name 以 李 开头只有两个字的数据。

正则表达式中没有 `%` 和 `_`，这是在 `LIKE` 中的用法。

???+ question
    1. 查找邮件地址以 zhangsan 开头的玩家。

    2. 查找邮件地址以 a/b/c 开头的玩家。

    3. 查找邮件地址以 net 结尾的玩家。

??? note "answer"
    1. `SELECT * FROM player WHERE email REGEXP '^zhangsan';`

    `SELECT * FROM player WHERE email LIKE 'zhangsan%';`

    2. `SELECT * FROM player WHERE email REGEXP '^[abc];`

    `SELECT * FROM player WHERE email REGEXP '^[a-c];`

    3. `SELECT * FROM player WHERE email REGEXP 'net$';`

    `SELECT * FROM player WHERE email LIKE '%net';`

---

### `IS NULL`

可以用 `IS NULL` 查询空值。

`SELECT * FROM player WHERE email IS NULL;` 用于查询 email 为空的数据。

不能使用 `= null`，因为 null 是一个特殊的值，表示未知，与其本身也不相等。

---

### `ORDER BY`

可以用 `ORDER BY` 排序。

`SELECT * FROM player ORDER BY level;` 用于查询 level 排序的数据。默认是升序，也可以显式地加上一个 `ASC`。

`SELECT * FROM player ORDER BY level DESC;` 用于查询 level 降序的数据。

`SELECT * FROM player ORDER BY level DESC, exp ASC;` 用于查询 level 降序，exp 升序的数据。

`SELECT * FROM player ORDER BY 5 DESC;` 用于查询第 5 列(也即 level 列)排序的数据。

---

### 聚合函数 and `GROUP BY`

!!! note "常用的聚合函数"
    - `AVG()` 平均值
    - `COUNT()` 计数
    - `MAX()` 最大值
    - `MIN()` 最小值
    - `SUM()` 求和

可以用 `GROUP BY` 分组。

`SELECT AVG(level) FROM player;` 用于查询 level 的平均值。

`SELECT sex, count(*) from player group by sex;` 用于查询每个性别的数量。

---

### `HAVING`

`HAVING` 可以用于对分组后的结果进行过滤。

`SELECT level, count(level) FROM player GROUP BY level HAVING count(level) > 10;` 用于查询 level 大于 10 的数量。

`SELECT level, count(level) FROM player GROUP BY level HAVING count(level) > 10 ORDER BY count(level) DESC;` 用于查询 level 大于 10 的数量，并按数量降序排序。

???+ question
    统计每个姓氏玩家的数量，并将结果按照数量来降序排列，只显示数量大于等于 5 的姓氏。

??? note "answer"
    ```sql
    SELECT SUBSTR(name, 1, 1) AS surname, COUNT(surname) FROM player GROUP BY surname HAVING count(surname) >= 5 ORDER BY COUNT(*) DESC;
    ```

---

### `LIMIT`

可以用 `LIMIT` 限制返回的行数。

```sql
SELECT SUBSTR(name, 1, 1) AS surname, COUNT(surname) 
FROM player 
GROUP BY surname 
HAVING count(surname) >= 5 
ORDER BY COUNT(*) DESC
LIMIT 3, 3;
```

- 如果只有一个 3 那么就是返回前 3 名。
- 如果是两个，那么第一个 3 是偏移量，表示从第 4 名开始。第二个 3 是返回的数量，所以这里是返回第 4 到第 6 名。

---

### `DISTINCT`

可以用 `DISTINCT` 去重。

`SELECT DISTINCT name FROM player;` 用于查询所有不同的名字。

---

### `UNION`

可以用 `UNION` 合并两个查询结果。

```sql
SELECT * FROM player WHERE level > 10
UNION
SELECT * FROM player WHERE exp BETWEEN 10000 AND 20000;
```

`UNION` 会自动去重，如果不想去重可以用 `UNION ALL`。

`UNION` 和 `OR` 有点类似，区别在于 `UNION` 是用来合并两个查询结果的，也即是取两个查询结果的并集。

---

### `INTERSECT`

可以用 `INTERSECT` 查询两个查询结果的交集。

```sql
SELECT * FROM player WHERE level > 10
INTERSECT
SELECT * FROM player WHERE exp BETWEEN 10000 AND 20000;
```

---

### `EXCEPT`

可以用 `EXCEPT` 查询两个查询结果的差集。

```sql
SELECT * FROM player WHERE level > 10
EXCEPT
SELECT * FROM player WHERE exp BETWEEN 10000 AND 20000;
```

---

## 子查询

`SELECT * FROM player where level > SELECT AVG(level) FROM player;`

`CREATE TABLE new_player SELECT * FROM player WHERE level > 10;`

`SELECT * FROM new_player;`

`INSERT INTO new_player SELECT * FROM player WHERE level BETWEEN 1 AND 5;`

`SELECT EXISITS(SELECT * FROM player WHERE level > 10);`

不存在时返回 0，存在时返回 1。

---

## 表关联

内连接只返回两个表中都有的数据。

左连接就是返回左表中所有数据和右表中匹配的数据，如果没有匹配的数据，右表中的数据为 NULL。

右连接就是返回右表中所有数据和左表中匹配的数据，如果没有匹配的数据，左表中的数据为 NULL。

```sql
SELECT * 
FROM player
INNER JOIN equip
ON player.id = equip.player_id;
```

---

## 索引

索引是一种用来提高查询效率的数据结构，可以帮助我们快速定位到想要的数据。如果没有索引就只能从头开始遍历，直到找到想要的数据。

`CREATE [UNIQUE|FULLTEXT|SPATIAL] INDEX idx_player_level ON player(level);`

一般来说，我们会为一张表的主键字段或者经常用来查询的字段用来索引。

`DROP INDEX idx_player_level ON player;`

`ALTER TABLE index_player ADD INDEX idx_player_level(level);`

---

## 视图

视图是一种虚拟表，它本身不存储数据，而是作为一个查询语句保存在数据字典中。根据查询语句的定义来动态地生成数据。

`CREATE VIEW top10 AS SELECT * FROM player ORDER BY level DESC LIMIT 10;`

视图中的数据是动态的，会随着表的数据变化而变化。

`ALTER VIEW top10 AS SELECT * FROM player ORDER BY level LIMIT 10;`

`DROP VIEW top10;`

---