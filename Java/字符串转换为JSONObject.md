##在Java中，如何将字符串转换为JSONObject

我有一个名为`jsonString`的字符串变量：

```
{"phonetype":"N95","cat":"WP"}
```

现在我想把它转换成JSON对象。已在Google上各种搜索查找，但没有得到任何预期的答案...



## 最佳解决方法

使用[org.json](https://mvnrepository.com/artifact/org.json/json)库：

```
JSONObject jsonObj = new JSONObject("{\"phonetype\":\"N95\",\"cat\":\"WP\"}");
```

或者：

```
JSONParser parser = new JSONParser();
JSONObject json = (JSONObject) parser.parse(stringToParse);
```