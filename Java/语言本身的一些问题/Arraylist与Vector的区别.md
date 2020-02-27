# Arraylist与Vector的区别

![img](https://pic3.zhimg.com/80/v2-76c3c04de2e8609c488fa0081fb99c26_hd.png)

这张图里的内容对我们学习Java来说，非常的重要，白色的部分是需要去了解的，黄色部分是我们要去重点了解的，不但要知道怎么去用，至少还需要读一次源码。绿色部分内容已经很少用了，但在面试题中有可能会问到，我们来看一个经常出现的面试题：**Arraylist与Vector的区别是什么？**

**首先我们给出标准答案：
1、Vector是线程安全的，ArrayList不是线程安全的。
2、ArrayList在底层数组不够用时在原来的基础上扩展0.5倍，Vector是扩展1倍。**

看上图Vector和ArrayList一样，都继承自List，来看一下Vector的源码

![img](https://pic2.zhimg.com/80/v2-053bbb6039358c7cde9a8decaa0435ad_hd.png)

实现了List接口，底层和ArrayList一样，都是数组来实现的。分别看一下这两个类的add方法，首先来看ArrayList的add源码

![img](https://pic2.zhimg.com/80/v2-b19db72823330f12eed436798e816591_hd.png)

再看Vector的add源码

![img](https://pic1.zhimg.com/80/v2-0fd2ad6622b8c236dc0497a4f02efb00_hd.png)

方法实现都一样，就是加了一个synchronized的关键字，再来看看其它方法，先看ArrayList的remove方法

![img](https://pic3.zhimg.com/80/v2-f170ed726954b56297d66f18723b1e22_hd.png)

再看Vector的remove方法

![img](https://pic3.zhimg.com/80/v2-4e8ad400f1cb2aeef1f4b58ad4a544be_hd.png)

方法实现上也一样，就是多了一个synchronized关键字，再看看ArrayList的get方法

![img](https://pic2.zhimg.com/80/v2-33fca77d43ecdb99234456ee032e31e5_hd.png)

Vector的get方法

![img](https://pic3.zhimg.com/80/v2-a6d3bbf74f90e3f31e607a831ae40aee_hd.png)

再看看Vector的其它方法

![img](https://pic2.zhimg.com/80/v2-f70120e40384d3fc4947085f08f37d9d_hd.png)

无一例外，**只要是关键性的操作，方法前面都加了synchronized关键字，来保证线程的安全性**。当执行synchronized修饰的方法前，系统会对该方法加一把锁，方法执行完成后释放锁，**加锁和释放锁的这个过程，在系统中是有开销的，因此，**在单线程的环境中，Vector效率要差很多。（多线程环境不允许用ArrayList，需要做处理）。

至于底层数组的扩容区别，这里就不带着大家读源码了，有兴趣的朋友大家自己读吧，底层代码几乎是一样的，不同的只是计算后的新数组长度不一致。

**和ArrayList和Vector一样，同样的类似关系的类还有HashMap和HashTable，StringBuilder和StringBuffer，后者是前者线程安全版本的实现。**希望以后大家在面试过程中，能说出个因为所以，而不是一味的去背面试题，唯有理解，无需再背。

注：关于线程安全性，后续文章会说，这里只是简单说这两个类不一样的地方。

上一篇：[ArrayList的时间复杂度 - 知乎专栏](https://zhuanlan.zhihu.com/p/28016098)

下一篇：[Java数据结构之线性表 - 知乎专栏](https://zhuanlan.zhihu.com/p/28346365)