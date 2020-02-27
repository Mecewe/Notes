# MySQL中添加唯一约束和联合唯一约束

在MySQL数据库中，经常会碰到由于业务需要添加唯一键约束，唯一键约束，可以在一个列上添加约束，也可以在多个列上添加唯一约束。



### 一、单列唯一约束

在一列上添加唯一约束，主要是让该列在表中只能有唯一的一行，例如注册邮箱时的邮箱名、手机号等信息，相关操作如下：

#### 1.建表时加上唯一性约束：

```mysql
CREATE TABLE `t_user` (
    `Id` int(11) NOT NULL AUTO_INCREMENT, 
    `username` varchar(18) NOT NULL unique, 
    `password` varchar(18) NOT NULL, 
    PRIMARY KEY (`Id`) 
) ENGINE=InnoDB AUTO_INCREMENT=1018 DEFAULT CHARSET=gbk; 
```

#### 2.给已经建好的表加上唯一性约束：

```mysql
ALTER TABLE `t_user` ADD unique(`username`);
```

或者：

```mysql
create unique index UserNameIndex on 't_user' ('username');
```

### 二、多列联合唯一约束

如果业务中要求两个字符联合起了是唯一的，比如“地址”+“名称”是唯一的，这就需要对两列，甚至多列添加联合唯一约束，具体命令如下：

#### 1.确认表结构

```mysql
mysql> show create table jw_resource;

FIELD          TYPE          COLLATION       NULL    KEY     DEFAULT  Extra           PRIVILEGES            COMMENT

-------------  ------------  --------------  ------  ------  -------  --------------  --------------------  -------

id             BIGINT(20)    (NULL)          NO      PRI     (NULL)   AUTO_INCREMENT  SELECT,INSERT,UPDATE         
resource_name  VARCHAR(128)  gbk_chinese_ci  YES             (NULL)                   SELECT,INSERT,UPDATE         
resource_type  TINYINT(4)    (NULL)          YES             (NULL)                   SELECT,INSERT,UPDATE 
```

#### 2.给resource_name和resource_type添加联合唯一约束：

```mysql
mysql> show index from jw_resource;

mysql> ALTER TABLE jw_resource
ADD UNIQUE KEY(resource_name, resource_type);
```

#### 3.确认表结构添加约束后结果：

```mysql
mysql>  show create table jw_resource;
CREATE TABLE `jw_resource` (
  `id` BIGINT(20) NOT NULL AUTO_INCREMENT,
  `resource_name` VARCHAR(128) DEFAULT NULL,
  `resource_type` TINYINT(4) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `resource_name` (`resource_name`,`resource_type`)
) ENGINE=INNODB AUTO_INCREMENT=2 DEFAULT CHARSET=gbk;

mysql> show index from jw_resource;
```

注意：唯一键约束添加后，在建表的元数据中，默认的唯一键约束名称为第一列的名称。

#### 4.添加约束后，进行插入测试效果：

```mysql
msyql> INSERT INTO `jw_resource`(`resource_name`,'resource_type') values('aa','11');

msyql> INSERT INTO `jw_resource`(`resource_name`,'resource_type') values('aa','22');

msyql> INSERT INTO `jw_resource`(`resource_name`,'resource_type') values('bb','11');

msyql> INSERT INTO `jw_resource`(`resource_name`,'resource_type') values('aa','11');
```

#### 5.删除唯一约束

```mysql
mysql> ALTER TABLE jw_resource DROP INDEX `resource_name`;

mysql> show index from jw_resource;
```

