# [Mysql设置字段唯一，值唯一方式](https://www.cnblogs.com/difs/p/9447199.html)

Mysql设置某字段唯一

 

### 1.建表时加上唯一性约束

```mysq
CREATE TABLE `t_user` (

`Id` int(11) NOT NULL AUTO_INCREMENT,

`username` varchar(18) NOT NULL unique,

`password` varchar(18) NOT NULL,

PRIMARY KEY (`Id`)  

) ENGINE=InnoDB AUTO_INCREMENT=1018 DEFAULT CHARSET=gbk;
```

### 2.给已经建好的表加上唯一性约束

```mysql
ALTER TABLE `t_user` ADD unique(`username`);
```



## **mysql主键索引和唯一索引**

- 1.主键一定是唯一性索引，唯一性索引并不一定就是主键；

- 2.一个表中可以有多个唯一性索引，但只能有一个主键；

- 3.主键列不允许空值，而唯一性索引列允许空值。