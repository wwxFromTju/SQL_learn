##### FROM的效果是：从筛选出来的表做笛卡尔积。然后依次遍历所有的元组，筛去不符合WHERE子句的元组

##### UNION 并
EXCEPT 差
INTERSECT 交
（NOT） EXISTS （不）存在
ALL 所有
ANY 任意一个

下面的可以用在having中，直接表示对分组的判断
ANY 任意一个
EVERY 全部

CONSTRAINT 限制
只能check本表内的，如果是多张表的话，用断言

```
CREATE TABLE Reserves( sname CHAR(10),bid INTEGER,day DATE,PRIMARY KEY (bid,day), CONSTRAINT noInterlakeRes CHECK (`Interlake’ <>( SELECT B.bname FROM Boats B WHERE B.bid=bid)))
```


ASSERTION 断言：在多个表中创建限制条件：

```
CREATE ASSERTION smallClubCHECK( (SELECT COUNT (S.sid) FROM Sailors S)+ (SELECT COUNT (B.bid) FROM Boats B) < 100 )
```

触发器

```
CREATE TRIGGER youngSailorUpdateAFTER INSERT ON SAILORS ------EventREFERENCING NEW TABLE NewSailorsFOR EACH STATEMENTINSERT INTO YoungSailors(sid, name, age, rating) ----ActionSELECT sid, name, age, ratingFROM NewSailors NWHERE N.age <= 18 ----Condition
```

