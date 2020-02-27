# 关于MYSQL的max_allowed_packet 超出的错误修复

错误信息：
com.mysql.jdbc.PacketTooBigException: Packet for query is too large (1201 > 1024). You can change this value on the server by setting the max_allowed_packet' variable.

开始以为是超出了字段的最大范围，网上查询后发现是mysql默认加载的数据文件不超过1M，可以通过更改mysql的配置文件my.cnf（Linux，或windows的my.ini）来更改这一默认值，从而达到插入大数据的目的。


docker下运行mysql

#### 1、进入docker容器中mysql

```shell
docker exec -it e871bdc484f1 mysql -uroot -p
#密码

```

#### 2、设置max_allowed_packet常量的大小

```sql
set global max_allowed_packet = 2*1024*1024*10;
```

#### 3、重启mysql服务，我这里用到的是docker集成的mysql

```shell
docker restart docker-ID
```

#### 4、在客户端连接使用一下语句进行查看

```sql
show VARIABLES like '%max_allowed_packet%';
```

  max_allowed_packet与slave_max_allowed_packet都会变大

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191226165448722.png" alt="image-20191226165448722" style="zoom:43%;" />

***主***最大允许包（max_allowed_packet），***从***最大允许包（slave_max_allowed_packet）

