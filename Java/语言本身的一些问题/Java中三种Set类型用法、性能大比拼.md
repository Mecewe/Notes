# Java中三种Set类型用法、性能大比拼

Java为开发者提供了大量的工具类，这给开发人员带来了很大方便，但是选择多了也有困扰，究竟用哪个类；我想选择什么，一是看自己具体需求，二是类本身的性能和用法；Java中提供了HashSet、TreeSet、LinkedHashSet三种常用的Set实现，以下具体分析它们的用法和性能。



我们使用Set的原因是**Set集合不包含重复元素**，HashSet、TreeSet和LinkedHashSet三种类型什么时候使用它们，使用哪个这是一个很重要的选择性问题，正确的选择会大大提升程序运行效率；

#### 总结一下：

##### 如你的需求是要一个能快速访问的Set，那么就要用HashSet

##### 如果你要一个排序Set，那么你应该用TreeSet

##### 如果你要记录下插入时的顺序时，你应该使用LinedHashSet。

把握这几个原则，是不是选择起来就简单多了。

Set接口的特性，Set接口继承了Collection接口，Set集合中不能包含重复的元素，每个元素必须是唯一的，你只要将元素加入set中，重复的元素会自动移除。下面分三方面对它的三个实现类进行说明。

#### 1、HashSet类：

HashSet是采用hash表算法来实现的，其中的元素没有按顺序排列，主要有add()、remove()以及contains()等方法；代码例子如下：

先定义一个实体类

```java
class Apple implements Comparable<Apple>{
    int size;

    public Apple(int s) {
    size = s;
    }

    public String toString() {
    return size + "";
    }

    @Override
    public int compareTo(Apple o) {
    return size - o.size;
    }
}

HashSet dset = new HashSet();
dset.add(new Apple(8));
dset.add(new Apple(1));
dset.add(new Apple(6));
dset.add(new Apple(7));
dset.add(new Apple(2));
Iterator iterator = dset.iterator();
while (iterator.hasNext()) {
System.out.print(iterator.next() + " ");
}
```



执行后输出：

8 6 2 1 7

可以看到这是没有顺序的。

![img](https://img-blog.csdn.net/20171101132909705?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYmVzdHhpYW9r/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

#### 2、TreeSet类：

TreeSet是采用树结构实现(称为红黑树算法)，元素是按顺序进行排列，主要有add()、remove()以及contains()等方法，它们都是复杂度为O(log (n))的方法；它还提供了一些处理排序的set方法，如first(), last(), headSet(), tailSet()等。代码例子如下：

```java
reeSet tree = new TreeSet();
 
tree.add(28);
 
tree.add(58);
 
tree.add(38);
 
tree.add(18);
 
Iterator iterator = tree.iterator();
 
System.out.print("排序后的数据显示: ");
 
while (iterator.hasNext()) {
 
System.out.print(iterator.next() + " ");
 
}
```

执行后输出如下：

排序后的数据显示: 18 28 38 58

#### 3、LinkedHashSet类：

LinkedHashSet正好介于HashSet和TreeSet之间，它也是一个hash表，但它同时维护了一个双链表来记录插入的顺序，基本方法的复杂度为O(1)。代码例子如下：

```java
LinkedHashSet dset = new LinkedHashSet();
 
dset.add(new Apple(7));
 
dset.add(new Apple(6));
 
dset.add(new Apple(8));
 
dset.add(new Apple(10));
 
dset.add(new Apple(9));
 
Iterator iterator = dset.iterator();
 
while (iterator.hasNext()) {
 
System.out.print(iterator.next() + " ");
 
} 
```

执行输出：7 6 8 10 9
输出的顺序和插入的顺序是一样的。

![img](https://img-blog.csdn.net/20171101133044450?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYmVzdHhpYW9r/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)