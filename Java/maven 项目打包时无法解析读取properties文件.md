# [maven 项目打包时无法解析读取properties文件](https://www.cnblogs.com/lianshan/p/5676963.html)

```
在做项目时遇见一个问题，无法解析properties文件的 内容   异常为
Could not resolve placeholder    .........
```

在此之前均有做相关的 配置 但是从未出现过如上异常，困惑了很久，最后把 war包提取出来得知  properties文件未被加载进项目中，因此无法识别。

但这的原因是为什么呢  ，原来此项目采用的是maven配置，但是maven在打包时将丢失properties文件,**原因maven执行compile是只会扫描*.class文件。**

那么这种请款添加如下配置即可。

```
   <resources>
      <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
        <includes>
          <include>**/*.xml</include>
          <include>*.properties</include>
        </includes>
      </resource>
    </resources>
```

**补充：** 

那么还有另外一中情况，如果我们在resource目录下添加了另一个cfg.ini文件我们希望将其也在我们的包结构中呈现那么这种情况我们应该如何配置呢？

```
<resources>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>     <!--替换文件内${}内的值为真实值-->
                <includes>
                    <include>**/*.xml</include>　　<!--只加载xml文件-->
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>false</filtering>
                <excludes>
                    <exclude>**/*.xml</exclude>       <!-- 所有的非xml文件都加载进来，不替换-->
                </excludes>
            </resource>
        </resources>
```

请注意我上面的两个配置，注意他们的区别，第一个为resource代表需要进行真实值的替换，包括下列文件，第二个为不需要进行真实值替换的包含的文件。

只有两个都包括，这样才会将properties ,xml ,  ini文件都加载到我们的项目包中。

**当然最简单的可以这样，一了百了**

```
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>
            </resource>
        </resources>
```