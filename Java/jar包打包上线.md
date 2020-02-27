mqtt-back-1

nohup java -jar mqtt-back-1.jar > runLog.file 2>&1 &

``````shell
nohup java -jar springboot-mybatis-1.0.1-SNAPSHOT.jar > runLog.file 
2>&1 &
``````

用nohup命令就好
spring-boot-1.0-SNAPSHOT.jar是你的 包名

然后这个runLog.file 是你运行时记录的日志

```shell
tail -f 100 runLog.file 
```

查看实时滚动的数据

```shell
vi runLog.file 
```

也可以用`vi`编辑器查看

我想关掉后台运行的 Spring Boot 的服务 我该怎么做呢：

``````shell
ps -ef | grep SpringBlade
``````





``````shell
ps aux | grep spring | xargs kill -9
``````

ps aux 是找出现在所有运行的进程
grep spring 是找出这些进程中名字是带有spring 字样的
xargs 将这个前面找到的名字传给后面这个kill -9这个命令
kill -9 就是强制删除进程了.



###Maven打包

https://blog.csdn.net/smilecall/article/details/56288972