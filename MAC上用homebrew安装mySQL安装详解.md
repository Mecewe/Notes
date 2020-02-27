### MAC上用homebrew安装mySQL安装详解

首先第一步：

`$ brew install mysql # 安装指定版本： brew install mysql@1.1.1`

接着等待安装，会有如下显示：

```l
==> mysql

We've installed your MySQL database without a root password. To secure it run:

​    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:

​    mysql -u root

To have launchd start mysql now and restart at login:

  brew services start mysql

Or, if you don't want/need a background service you can just run:

  mysql.server start
```

如果按提示直接运行``mysql_secure_installation``会出现以下问题：

![image-20190727221353869](/Users/mecewe/Library/Application Support/typora-user-images/image-20190727221353869.png)

所以需要先执行以下步骤：

``$ mysql.server start``

再执行以下步骤：

``$ mysql_secure_installation``

出现以下部分：

```
Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: Y   ## 回复y 需要密码8位以上，回复n 则不做限制

The password validation component is not available. Proceeding with the further steps without the component.
Please set the password for root here.

New password:   ## 设置你的密码

Re-enter new password:   ## 再次输入你的密码

By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y    ## 是否移除匿名用户。考虑安全我选了y
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y   ## 是否允许远程连mysql 的 root。我用做本地调试，不是远程服务器，所以y了
Success.

By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.

Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y      ## 是否y了删除test数据库，我选了y
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y      ## 选y, 重新加载权限列表
Success.

All done!
```



到此配置就结束了，下面我们启动 mysql 即可，记住以下命令：

```
$ mysql -u root -p   ## 登陆 mysql
$ brew services start mysql@5.7   ## 启动 mysql
$ brew services stop mysql@5.7   ## 停止 mysql
$ mysql.server start   ## 启动 mysql(无后台服务)
```



另外使用navicat连接出现以下问题：

![image-20190727222714977](/Users/mecewe/Library/Application Support/typora-user-images/image-20190727222714977.png)





**解决**

终端登录 mysql，执行下面的命令：

```ALTER
USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';
```