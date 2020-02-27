

# js将yyyymmddhhmmss字符转换为Date

### 方法一

原字符串20160928171823需要转换为Date日期格式

```javascript
//1、首先将20160928171823转换为可以被Date识别的格式 2016/09/28 17:18:23
var dateString="20160928171823";
var pattern = /(\d{4})(\d{2})(\d{2})(\d{2})(\d{2})(\d{2})/;
var formatedDate = dateString.replace(pattern, '$1/$2/$3 $4:$5:$6');
//2、将字符串 2016/09/28 17:18:23转换为Date日期格式
var ddate = new Date(formatedDate);
```

### 方法二

```javascript
String datetime =  "20140212111012";
DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyyMMddHHmmss");
LocalDateTime ldt = LocalDateTime.parse(datetime,dtf);
System.out.println(ldt);//2014-02-12T11:10:12

DateTimeFormatter fa = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
String datetime2 = ldt.format(fa);
System.out.println(datetime2);//2014-02-12 11:10:12
```

