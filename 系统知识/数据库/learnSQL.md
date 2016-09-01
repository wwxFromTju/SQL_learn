# SQL学习整理
## 相应知识点只适用于Mysql

### SQL 语句模版
查询

* SELECT xx
* FROM xx
* WHERE xx
* GROUP BY xx
* HAVING XX
* ORDER BY xx 

执行顺序：FROM 笛卡尔积， 然后WHERE筛选掉不符合的元组， 然后GROUP BY划分元组， HAVING筛选掉不符合的划分出来的元组，然后就是ORDER BY元组， 最后是SELECT投影。

插入

``` 
INSERT INTO Customers(col-name...) 这部分字段名可以省略，但是省略就插入所有的和表一样的字段了
 VALUES(...) 
```

更新数据

* UPDATE xxx
* SET xxx = xxx
* WHERE xxx

删除数据

* DELETE FROM xxx
* WHERE xxx

创建表
```
CREATE TABLE xxx
(
xxx type （NOT） NULL DEFAULT xxx CHECK (要求 ),
...
PRIMARY KEY (....)
FOREIGN KEY (...) REFERENCES 表名(...)
)
```

创建视图
```
CREATE VIEW ... AS
SELECT ...
FROM ...
WHERE ...
...
```

更新表结构
```
ALTER TABLE xxx
ADD COLUMN xxx type ....
ADD FOREIGN KEY(...) REFERENCES 表名(...);
```
```
ALTER TABLE xxx
DROP COLUMN xxx;
```

删除整个表
```
DROP TABLE xxx;
```

创建索引
```
CREATE INDEX 索引名
ON 表名（字段名...）
```

创建触发器
```
CREATE TRIGGER trigger_name
trigger_time
trigger_event ON tbl_name
FOR EACH ROW
BEGIN
trigger_stmt
END
取值
trigger_time：BEFORE，AFTER
trigger_event：INSERT，UPDATE，DELETE
```

事务
```
START TRANSACTION;
...
...
SAVEPOINT xxx(时间点)
...
COMMIT/ROLLBACK;(或者ROLLBACK TO xxx时间点)
```

创建用户
```
CREATE USER 用户名 IDENTIFIED BY '密码'
```

修改用户名
```
RENAME USER 旧用户名 TO新用户名
```

删除用户
```
DROP USER 用户名
```

显示访问权限
```
SHOW GRANTS FOR 用户名
```

赋权
```
GRANT 操作(select...) ON 数据库名.表名(*代表全部) TO 用户名
```

收回权限
```
REVOKE 操作(select...) ON 数据库名.表名(*代表全部) FROM 用户名
```

修改密码
```
SET PASSWORD FOR 用户名 = Password('新密码')
```

修改自己密码
```
SET PASSWORD = Password('新密码')
```


### 检索数据

##### SQL不区分大小写，不只是select这类的关键字不区分大小写，包括表名，字段名也都不区分大小，但是建议关键字大写，然后其他和你创建的字段名一致最好，同时最好采用分行的方式进行书写。

##### DISTINCT关键字应该放在第一个字段那里，效果为去掉重复的row。 把DISTINCT换为ALL是显式地指定保留下重复的列。

##### 可以在SQL语句的后面加上LIMIT语句，可以限制选取出来的row的个数，默认是从头开始，可以配置OFFSET来设置从第几行往下开始选去，0为从头开始

##### 可以使用 -- 和 # 创建单行注释，-- 创建的注释要空一格，再开始写，使用 /* xxx */ 创建多行注释


### 排序检索数据

#####  默认SELECT出来的数据的顺序是不可以假设的，要明确指定之后才能确定。

##### 可以通过 ORDER BY 语句指定排序的row，默认是升序排列asc，在字段后面加上 DESC 可以指定为降序排列（只影响加上去的字段，其他没有加的依旧是升序）。可以任意指定字段，可以选择没有SELECT出来的字段。可以同时指定多个排序的字段，优先级依次下降。

##### 在 ORDER BY 的时候，可以指定字段名，也可以通过SELECT出来的位置信息来排序，选出字段从1开始计数


### 过滤数据

##### 使用 WHERE 关键字添加筛选row的条件。 大部分和编程语言的大小判断类似，特殊的： BETWEEN x1 AND x2： 在 x1 和 x2 内 ( x1 <= x2 )。 IS NULL 判断是不是为NULL。 <> 不等于。 ！> 不大于。 ！< 不小于。 (!>, !< 在mysql中不支持)

##### 注意比较时候的数据类型，特别是字符串和数字的区别，最好转换之后再比较_todo_ ：这个还没搞清楚

##### 空值NULL不能简单地 = NULL， 任何直接和NULL比的话结果是NULL。 所以使用 IS NULL 和 IS NOT NULL


### 高级数据过滤

##### 使用 AND 添加 且 条件, 使用 OR 添加 或条件, 注意 AND 的优先级大于 OR， 书写时候最好加上（）来指定优先级

##### 使用 IN 来判断是否在相应的范围内， 比如 price in （ 100， 200 ）, 类似于简化的 OR , 对应 NOT IN 来判断是否不在里面

##### 使用 NOT 来否定后面的条件判断

##### 如果使用嵌套查询，查询出一系列值，可以使用IN或者NOT IN来判断是否在里面， 如果是大小，不等之类的判断， 可以使用 > ALL(...) 比选出来的所有都大, > ANY(...)比选出来的任意一个都大。EXISTS 判断是否存在， NOT EXISTS：判断是否不存在。


### 用通配符进行过滤

##### 使用 LIKE 来进行通配， % 对应任意字符的任意次数， _ 匹配任意字符的一次


### 创建计算字段

##### 字符串拼接使用 CONCAT 函数

##### 使用 RTRIN 函数去掉右边的空白， LTRIN 函数去掉左边的空白， TRIN 函数去掉左右的空白

##### 使用 AS 来指定计算字段的别名, 也可以直接空格之后使用别名

##### SELECT 中可以计算，比如用单价和数量计算总价


### 使用函数处理数据

##### 文本处理函数
*  UPPER 转为大写
*  LOWER 转为小写
*  LENGTH 计算字符串长度
*  SOUNDEX 返回一个值，读音相同的值相同

##### 日期处理函数
* YEAR 获得日期中的年

##### 数值处理函数
* ABS 绝对值
* COS 一个角度的余弦, 是角度制
* EXP 返回一个数的e的指数值
* PI 返回圆周率
* SIN 一个角度的正弦
* SQRT 平方根
* TAN 一个数的正切


### 汇总数据

##### 通常出现了聚集函数，则不应该出现GROUP BY中没有字段，而且不能直接在WHERE中使用聚合函数，如果需要使用数值的话，那么应该是嵌套查询出一个数值

##### 聚集函数 默认忽略 NULL
* AVG 平均值
* COUNT 统计行数
* MAX 最大值
* MIN 最小值
* SUM 总和

##### 在聚合函数中，默认是不去掉的重复值的，如果需要去掉重复值，则在字段前面加上 DISTINCT, 但是不能在 ＊ 前面加 DISTINCT


### 分组数据

##### 使用 GROUP BY 进行数据分组, 聚合函数是作用来分组上的， 所以会有多个值

##### 使用HAVING 来对分组加筛选条件, 只能添加筛选的为 GROUP BY 中指定的字段或聚合函数


### 使用子查询

##### 通过利用 SELECT 语句来先筛选出数据，然后将这些数据利用起来，记得使用括号

##### 子查询只能返回一列的数据，不能返回多个字段

##### 如果子查询中用到了多个表，那么使用字段的时候最好加上完全限定名， 即对应的表名


### 联结表

##### 可以使用 JOIN 进行联结，也可以选出表来，然后使用 WHERE 来判断条件相等，然后联结

##### 默认情况下，选取多个表是会形成笛卡尔积(也叫cross join 叉联结)，然后通过联结来限定条件

##### 表一 JOIN 表二 ON 条件，通过条件来筛选出来符合行，然后进行联结

##### 通常情况下是使用 equal join （等值联结）， 也叫 inner join（内联结）

##### 多个表联结类似2个表，可以在 WHERE 语句中使用多个条件判断，但是这样效率很低，同样的结果也可以使用 IN 


### 创建高级联结

##### self-join（自联结）， naturaljoin（自然联结）， 外联结（outer join）

##### self-join 就是同一张表之间的联结，这个时候应该使用别名，或者使用子查询

##### 自然联结：默认将联结的表中字段相同的进行联结

##### 外联结：就是可以保留没有匹配的，LEFT JOIN 就是可以保留左边没有匹配的，那么右边就可以为NULL， 同理，RIGHT JOIN 就是可以保留在右边没有匹配的，那么左边就可以为NULL

##### 可以将联结和分组结合起来，本质上就是先过滤出条件，进行联结，然后再分组。就可以使用聚集函数


### 组合查询

##### UNION 就是 或，类似在WHERE中使用 OR ，注意是按照位置进行 UNION 的，不是按照你 SELECT 出来的字段名，这个是默认去掉重复的行的，如果是使用 UNION ALL 是保留下来全部的行的(MYSQY中不支持INTERSECT／EXCEPT）

##### 可以在最后的地方对整个结果进行排序


### 插入数据

##### 看上面的模版，在表名后面最好加上字段名，也可以不加，对于可以是NULL，可以不加上去。

##### 可以复制表来直接创建表
* CREATE TABLE xxx AS
* SElECT ...
* FROM ....
* ... 这里是正常的WHERE， GROUP BY等语句都可以使用，也可以从多个表


### 更新和删除数据

##### 更新数据
* UPDATE ...
* SET xxx = xxx
* WHERE xxx

##### 删除数据
* DELETE FROM xxx
* WHERE xxx

注意一下WHERE子句，不然所有行都会被更新


### 创建和操纵表

##### 看上面的结构


### 使用视图

##### 本质上就是保存一些常用的 SELECT 语句，视图可以嵌套，不要使用 GROUP BY 子句， 不能被索引， 最好不要插入，


### 事务

##### 就是为了保证原子行，要不都执行成功，要不都不执行。


### 索引

##### 本质上数据库对于主键进行了排序，所以对主键查询快，但是对其他的字段则是无序的，也没有额外的文件来记录顺序，所以如果对其他的字段（可以是多个字段）查询多的话，那么可以考虑采用增加索引来加速查询速度

##### 注意条件
* 虽然增加了查询的速度，但是会降低插入，修改，删除的性能，因为这些操作时候，必须动态更新索引
* 索引需要占空间
* 如果数据范围小的话，比如只有1，2，3， 那么其实索引的效果很差，不如［1，100000］效果好
* 如果对某个字段进行过滤或者数据排序，然后推荐使用索引
* 如果是对多个字段使用的话，那么可以对多个字段进行索引，但是索引只对同时使用这多个字段时候有效，只使用其中子集部分无效。


###  触发器

##### 

