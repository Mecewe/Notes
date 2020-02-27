## 第六章

https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/ps.html

### ls

`ls -l`显示最后改动时间

###less

查看文件内容

``less 文件名``

> 操作方式
>
> <b> <space> <q>
>
> shift+g移动到最后一行
>
> ctrl+b往前一页一页翻页查看
>
> 
>
> /serchContent                – 使用一个模式进行搜索，并定位到下一个匹配的文本
> n                                     – 向前查找下一个匹配的文本
> N                                     – 向后查找前一个匹配的文本

#####分页程序

``less more pg ``

> **搜索**
>
> /pattern 向下搜索特定模式
>
> ？pattern 向上搜索特定模式
>
> / 向下搜索上一模式
>
> n 向下搜索上一模式
>
> ？向上搜索上一模式
>
> N 向上搜索上一模式
>
> **移动**
>
> g 移到页的顶部
>
> G 移到页的底部

### reboot和shutdown

重启系统

``sudo reboot 或者 sudo init 6``

关闭系统

``sudo shutdown now或者 sudo init 0``



### 环境变量printenv

显示环境变量

``printenv``



### 操作快捷键

> ^W 删除一个单词
>
> ^U 删除整行
>
> ^H 删除最后一个键入的字符，同<backSpace>
>
> ^S stop信号 暂停屏幕显示
>
> ^Q start信号 重新启动屏幕显示
>
> ^D eof(end of file)信号
>
> ^Z 挂起程序 通过fg命令恢复
>
> ^M  <=等价于=> <Return> 输入命令行后自动转化成 ^J
>
> ^J （newLine）新行字符 Unix以此标记每行结束
>
> reset命令 重置映射命令

### which

返回执行位置

``which 程序名``

### type

同which，返回执行位置

``type 程序名``

### 常用程序命令

>``date`` 显示时间和日期
>
>``cal`` 显示日历 ``cal 2019`` 年度日历
>
>``who`` 显示每个用户的信息

### man

查看各种命令

``man 联机手册中的条目``

### info

info系统

``info 命令 `` 



###tail

`tail`*命令会保持活动状态，并不断显示添加到文件中的内容。这是实时监测系统日志的绝妙方式。*









> 自己补充

### ps

`ps 参数`以下列一些常用的参数：

- -l ：long 表示显示进程的更多信息，包括PID，PPID等
- -A：All 显示所有的进程
- f：显示进程之间的关系树
- x：列出进程的STAT和启动的详细命令
- u：主要是能以百分比方式显示CPU使用率和内存使用率

`ps -l`

>信息的相关含义如下：
>
>- F：process flags 进程标识。
>- S：state 进程状态。其中D表示uninterruptible sleep；R表示runing或者runnable；S表示sleeping；T表示stop或者traced，进程停止或追踪状态；Z表示Zombie，僵尸进程。
>- UID：user id 进程拥有者的编号。
>- PID：process id 进程编号。
>- PPID：parent process id 父进程编号。
>- C：cpu使用率。
>- PRI：priority 进程的优先执行权，数值越高，优先权越小。
>- TTY：表示终端的设备编号
>- TIME：使用cpu的时间
>- CMD：进程的运行命令

`ps u -A` 看看消耗比较大的进程

![linux下ps命令测试截图4](http://cdn.01happy.com/wp-content/uploads/2012/11/linux%E4%B8%8Bps%E5%91%BD%E4%BB%A4%E6%B5%8B%E8%AF%95%E6%88%AA%E5%9B%BE4.png)

