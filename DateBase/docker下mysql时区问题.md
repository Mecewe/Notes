## docker下mysql时区问题

#### 1、创建mysql容器

```shell
docker run --name mysql -p 3306:3306 -v /home/mysql/data:/var/lib/mysql -v /home/mysql/conf.d:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7.28
```

#### 2、修改时区

通过date命令查看时间

查看主机时间

```
[root@localhost ~]# date
2016年 07月 27日 星期三 22:42:44 CST
```

查看容器时间

```
root@b43340ecf5ef:/#date                                                                                                                          
Wed Jul 27 14:43:31 UTC 2016
```

[Docker 解决容器时间与主机时间不一致的问题三种解决方案](https://m.jb51.net/article/99906.htm)

**2.1 共享主机的localtime (方法一)**

创建容器的时候指定启动参数，挂载localtime文件到容器内 ，保证两者所采用的时区是一致的。

```
docker run --name <name> -v /etc/localtime:/etc/localtime:ro .... 
```

**2.2复制主机的localtime (方法二)**

```shell
#有误
docker cp /etc/localtime 【容器ID或者NAME】:/etc/localtime
```

会报以下错误：

```shell
[root@localhost etc]# docker cp /etc/localtime b76bf62fe57e:/etc/
Error response from daemon: Error processing tar file(exit status 1): invalid symlink "/etc/localtime" -> "../usr/share/zoneinfo/Asia/Shanghai"
```

**成功解决方法：** 

```shell
docker cp /usr/share/zoneinfo/Asia/Shanghai 2c87bcc41378:/etc/localtime
#重启mysql 容器
docker restart 2c87bcc41378
```

在完成后，再通过date命令进行查看当前时间。

但是，在容器中运行的程序的时间不一定能更新过来，比如在容器运行的MySQL服务，在更新时间后，通过sql查看MySQL的时间

```
select now() from dual;
```

可以发现，时间并没有更改过来。

这时候必须要重启mysql服务或者重启Docker容器，mysql才能读取到更改过后的时间。

**2.3创建自定义的dockerfile (方法三)**

创建dockerfile文件，其实没有什么内容，就是自定义了该镜像的时间格式及时区。

```
FROM redis

FROM tomcat

ENV CATALINA_HOME /usr/local/tomcat

#设置时区
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
  && echo 'Asia/Shanghai' >/etc/timezone \
```

保存后，利用docker build命令生成镜像使用即可。

GRANT all ON. TO 'root'@'%' IDENTIFIED BY 'jiaosi502'; 