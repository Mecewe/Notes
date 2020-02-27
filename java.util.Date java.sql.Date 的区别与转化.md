###[java.util.Date java.sql.Date 的区别与转化](https://www.cnblogs.com/wu-fm/p/8608209.html)

```
共同点：都有getTime方法返回毫秒数，可以直接构建
**不同点：**
1、java.sql.Date是针对SQL语句使用的，它只包含日期而没有时间部分，一般在读写数据库的时候用，PreparedStament的setDate()的参数和ResultSet的getDate()方法的都是java.sql.Date
2、java.util.Date是在除了SQL语句的情况下面使用，一般是日常日期字段
```

`3、java.util.Date 是 java.sql.Date 的父类，`即：

继承关系：java.lang.Object —> java.util.Date —> java.sql.Date

**相互转化：**

```java
java.sql.``Date``转为java.util.``Date
java.sql.``Date` `date``=new java.sql.``Date``();
java.util.``Date` `d=new java.util.``Date` `(``date``.getTime());
java.util.``Date``转为java.sql.``Date
java.util.``Date` `utilDate=new ``Date``();
java.sql.``Date` `sqlDate=new java.sql.``Date``(utilDate.getTime());
java.util.``Date` `utilDate=new ``Date``();
java.sql.``Date` `sqlDate=new java.sql.``Date``(utilDate.getTime());
java.sql.``Time` `sTime=new java.sql.``Time``(utilDate.getTime());
java.sql.``Timestamp` `stp=new java.sql.``Timestamp``(utilDate.getTime());
**这里所有时间日期都可以被SimpleDateFormat格式化format()**
SimpleDateFormat f=new SimpleDateFormat(``"yyyy-MM-dd hh:mm:ss"``);
f.format(stp);
f.format(sTime);
f.format(sqlDate);
f.format(utilDate)
java.sql.``Date` `sqlDate=java.sql.``Date``.valueOf(``" 2005-12-12"![搜索](https://gss0.bdstatic.com/70cFsjip0QIZ8tyhnq/img/iknow/qb/select-search.png)``);
utilDate=new java.util.``Date``(sqlDate.getTime());
**另类取得年月日的方法：**
import java.text.SimpleDateFormat;
import java.util.*;
java.util.``Date` `date` `= new java.util.``Date``();
**如果希望得到YYYYMMDD的格式SimpleDateFormat**
sy1=new SimpleDateFormat(``"yyyyMMDD"``);
String dateFormat=sy1.format(``date``);
**如果希望分开得到年，月，日SimpleDateFormat**
sy=new SimpleDateFormat(``"yyyy"``);
SimpleDateFormat sm=new SimpleDateFormat(``"MM"``);
SimpleDateFormat sd=new SimpleDateFormat(``"dd"``);
String syear=sy.format(``date``);
String smon=sm.format(``date``);
String sday=sd.format(``date``);
```

