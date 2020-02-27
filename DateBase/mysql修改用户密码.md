## docker——mysql修改用户密码

> ”Access denied for user ‘root’@’localhost’ (using password: YES)”

# 正文

进入mysql报错:1045(28000)， 原因：mysql5.7 首次安装后，需要修改root的默认密码才能使用。

为了解决这个问题，来来回回试了很多遍，这里就不说过程了，下面记录下目前看正确的处理步骤：

## docker安装Mysql

1 docker拉取mysql版本：

> **docker pull mysql:5.7.23**

2 创建挂载目录：

> **mkdir /usr/local/mysql**

用于挂载mysql数据文件

> **mkdir /usr/local/mysql/data**

用于挂载mysql配置文件

> **mkdir /usr/local/mysql/conf.d**

3 启动容器

命令：

> docker run --name mysql5.7 -p 3306:3306 -v /usr/local/mysql/data:/var/lib/mysql -v /usr/local/mysql/conf.d:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=rootroot -d mysql:5.7.23

注意： -e MYSQL_ROOT_PASSWORD 这里==敲错了==，后面就是为了解决不知道root密码情况下怎么处理。

## 处理mysql 1045报错

1 在 /usr/local/mysql/conf.d目录下增加文件： my.cnf

文件内容为：

> [mysqld]
>  skip-grant-tables

2 重启mysql：

> docker restart mysql5.7

3进入docker的bash：

> docker exec -it mysql5.7 bash

4登录mysql：

> mysql -uroot -p

5设置root密码为空，注意root密码是加密的，设置其它值不好找到对应的明文。

> use mysql;
>
> select user,authentication_string,host from user;

//更新为空

> update user set authentication_string='' where user='root';
>
> flush privileges;

6 退出mysql，把第一步的skip-grant-tables注释。再重启mysql

7 使用 root用户，密码 回车键登录；

8 修改root密码：

> alter user 'root'@'localhost' IDENTIFIED BY 'rootroot'；
>
> alter user 'root'@'%' IDENTIFIED BY 'rootroot'；
>
> flush privileges；

修改root密码完成。

9 可附加一步授权：

> GRANT all ON \*.\* TO 'root'@'%' IDENTIFIED BY 'rootroot' ；
>
> flush privileges；

