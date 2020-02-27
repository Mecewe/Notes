##如何使用LocalDateTime解析/格式化日期？ (Java 8)

**解析日期和时间**

要从字符串创建`LocalDateTime`对象，可以使用静态`LocalDateTime.parse()`方法。它需要一个字符串和一个`DateTimeFormatter`作为参数。 `DateTimeFormatter`用于指定日期/时间模式。

```
String str = "1986-04-08 12:30";
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
LocalDateTime dateTime = LocalDateTime.parse(str, formatter);
```

**格式化日期和时间**

要从`LocalDateTime`对象中创建格式化的字符串，可以使用`format()`方法。

```
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
LocalDateTime dateTime = LocalDateTime.of(1986, Month.APRIL, 8, 12, 30);
String formattedDateTime = dateTime.format(formatter); // "1986-04-08 12:30"
```

请注意，在`DateTimeFormatter`中有一些常用的日期/时间格式被预定义为常量。例如：使用`DateTimeFormatter.ISO_DATE_TIME`格式化上面的`LocalDateTime`实例将产生字符串`"1986-04-08T12:30:00"`。

`parse()`和`format()`方法适用于所有日期/时间相关的对象(例如`LocalDate`或`ZonedDateTime`)