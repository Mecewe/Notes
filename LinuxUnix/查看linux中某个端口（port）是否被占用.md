# 查看linux中某个端口（port）是否被占用

1.使用lsof

```shell
lsof -i:端口号查看某个端口是否被占用
```

2.使用netstat

```shell
netstat -anp|grep 80
```

可以通过netstat -tulnp | grep 端口号查看当前端口号是否被占用



杀死线程

```shell
kill -9 PID
```





```shell
#安装
yum install telnet
#发送tcp数据
telnet ip port
```





```shell
#安装nc
yum install -y nc

#接收tcp
nc -l
```





```shell
netstat -tulnp

-t(tcp)只显示tcp相关的

-u(udp)只显示udp相关的

-l(listening)只显示监听服务的端口

-n(numeric)不解析名称,能用数字表示的就不用别名(例如:localhost会转成127.0.0.1)

-p(programs)显示端口的PID和程序名称
```

