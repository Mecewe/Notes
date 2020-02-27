# mysql字符集和排序规则

### 1.关于字符集和排序规则

所为字符集，就是用来定义字符在数据库中的编码的集合。常见的字符集有：utf8（支持中文）和AccIS（不支持中文）

数据库中的排序规则用来定义字符在进行排序和比较的时候的一种规则。常见的如下：
（1） utf8_general_ci 不区分大小写，utf8_general_cs 区分大小写
（2） utf8_bin 规定每个字符串用二进制编码存储，区分大小写，可以直接存储二进制的内容

说明：所为排序规则，就是指字符比较时是否区分大小写，以及是按照字符编码进行比较还是直接用二进制数据比较。

utf8_unicode_ci和utf8_general_ci对中、英文来说没有实质的差别。
utf8_general_ci校对速度快，但准确度稍差。
utf8_unicode_ci准确度高，但校对速度稍慢。

如果你的应用有德语、法语或者俄语，请一定使用utf8_unicode_ci。一般用utf8_general_ci就够了。

##### 所以一般字符集用utf-8，排序规则用utf8_general_ci

### 2、继承关系

mysql对服务器的每个数据库、每个表都有默认的字符集和排序规则。这形成了创建列时影响其字符集的默认值的继承关系。
在继承的每一个层次，都可以显示的定义字符集或让服务器使用默认值：
1.当创建一个数据库的时候，他从服务器继承了character_set_server设置；
2.当创建表的时候，他从数据库继承字符集；
3.当创建列时，它从表继承字符集；

### 3、查看字符集和排序规则有关的系统变量

字符集

```sql
show variables like 'character\_set\_%'; 
```

排序规则

```sql
show variables like 'collation\_%';
```

### 4、各系统变量含义

character_set_system：MySQL数据库标识符使用的字符集，永远是utf8
character_set_server和collation_server：服务器的默认字符集和排序方式
character_set_database和collation_database：当前数据库的默认字符集和排序方式
以下三个变量将影响客户端和服务器之间的通信：
character_set_client：客户端向服务器发送SQL语句使用的字符集
character_set_results：服务器向客户端返回结果时使用的字符集
character_set_connection：如果它和character_set_client不同，从客户端发来的SQL语句将转换为它指定的字符集
默认情况下，上述三个变量都设为为相同的值，

### 5、修改默认字符集和排序规则

其实也就是修改服务器端的。这样下面3层都会继承。
这里打算修改字符集为utf-8，排序规则为utf8_general_ci


打开mysql安装目录下my.ini文件，在最下面添加（mysqld组下）

character-set-server=utf8
collation_server=utf8_general_ci
![img](https://img-blog.csdn.net/20170619221954038?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzI0ODY1OTk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

**保存my.ini。关闭mysql服务器，重新打开。再用navicat查询工具输入上面的查询语句即可看到修改成功。**