# Mysql 存在既更新，不存在就添加（sql语句）

INSERT 语句的一部分,如果指定 ON DUPLICATE KEY UPDATE ，并且插入行后会导致在一个UNIQUE索引或PRIMARY KEY中出现重复值，则在出现重复值的行执行UPDATE，如果不会导致唯一值列重复的问题，则插入新行



### 方式一：

**比较合适的方法**：

```sql
INSERT INTO test VALUES (1,'b4','c4') ON DUPLICATE KEY UPDATE b=VALUES(b),c=VALUES(c);
```

**可以把上面的SQL简单的理解为**：

```sql
select count(1) from test where a=1;
if count(1) > 0
UPDATE test SET b='xxx',c='xxx' WHERE a=1;
```

可以看到有两行收到影响（至于为什么两行收到影响，就得研究底层的实现了，可以参考[官方文档](https://dev.mysql.com/doc/refman/5.7/en/insert-on-duplicate.html)）：



sql 语句原型：
insert into table (player_id,award_type,num)  values(20001,0,1) on  DUPLICATE key update num=num+values(num)

在工作中抽奖程序需要模仿王者荣耀钻石夺宝（满200幸运值  201抽中大奖  ）



实现思路：

  如果没有用户幸运值改变+1  ，新表中没有用户信息就添加

 1、判断用户信息是否存在 （不存在添加）

 2、存在修改用户幸运值个数

为了预防高并发下 两层sql出现问题

原sql : 

 select  num  from 表名 where  uid=20001 and  award_type=0 limit 1;

 update 表明 set  num=num+1 where  uid=20001 and  award_type=0



需求：

    uid和award_tyhpe两个字段值 都相同时才更新  其中有一个不一样就添加新数据

 效果展示：

![img](https://img-blog.csdn.net/20170713172546184)

执行语句  insert into table (player_id,award_type,num)  values(20001,0,1) on  DUPLICATE key update num=num+values(num)

![img](https://img-blog.csdn.net/20170713172606728)



insert into table (player_id,award_type,num)  values(20011,0,1) on  DUPLICATE key update num=num+values(num)

![img](https://img-blog.csdn.net/20170713172715271)



将player_id 、award_type  建立 联合unique 索引  

CREATE TABLE `willow_player` (
  `id` bigint(11) NOT NULL AUTO_INCREMENT,
  `player_id` bigint(16) NOT NULL DEFAULT '0',
  `num` int(11) NOT NULL DEFAULT '0',
  `award_type` tinyint(4) NOT NULL DEFAULT '0' COMMENT '类型',
  `repeat_num` smallint(11) NOT NULL DEFAULT '0' COMMENT '重复轮数',
  PRIMARY KEY (`id`),
  UNIQUE KEY `num` (`player_id`,`award_type`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=96 DEFAULT CHARSET=utf8mb4;

 

这样只有两个字段值内容全部一样时才会更新！！！   注意  id 会跳跃哦  mysql 机制原因





### 方式二：

讨人喜欢的 MySQL replace into 用法（insert into 的增强版）
在向表中插入数据的时候，经常遇到这样的情况：1. 首先判断数据是否存在； 2. 如果不存在，则插入；3.如果存在，则更新。

在 SQL Server 中可以这样处理：

   if not exists (select 1 from t where id = 1)
      insert into t(id, update_time) values(1, getdate())
   else
      update t set update_time = getdate() where id = 1
那么 MySQL 中如何实现这样的逻辑呢？别着急！mysql 中有更简单的方法： replace into

replace into t(id, update_time) values(1, now());
或

replace into t(id, update_time) select 1, now();
replace into 跟 insert 功能类似，不同点在于：replace into 首先尝试插入数据到表中， 1. 如果发现表中已经有此行数据（根据主键或者唯一索引判断）则先删除此行数据，然后插入新的数据。 2. 否则，直接插入新数据。

要注意的是：插入数据的表必须有主键或者是唯一索引！否则的话，replace into 会直接插入数据，这将导致表中出现重复的数据。

MySQL replace into 有三种形式：
1. replace into tbl_name(col_name, ...) values(...)
2. replace into tbl_name(col_name, ...) select ...
3. replace into tbl_name set col_name=value, ...
前两种形式用的多些。其中 “into” 关键字可以省略，不过最好加上 “into”，这样意思更加直观。另外，对于那些没有给予值的列，MySQL 将自动为这些列赋上默认值。