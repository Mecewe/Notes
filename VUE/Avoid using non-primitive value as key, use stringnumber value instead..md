# vue报错信息（Avoid using non-primitive value as key, use string/number value instead.）

避免使用非原始值作为关键字，而使用字符串/数字值代替。

解决方法：

![img](https://img-blog.csdn.net/20180802144258196?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NvdV92eXA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

for循环中，绑定的key值不能为对象，而是取一个字符串或数值，如下图：

![img](https://img-blog.csdn.net/20180802144429218?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NvdV92eXA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


