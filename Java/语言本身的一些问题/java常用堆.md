# [【Java】 用PriorityQueue实现最大最小堆](https://www.cnblogs.com/yongh/p/9945539.html)

**PriorityQueue（优先队列），一个基于优先级堆的无界优先级队列。**

实际上是一个堆（不指定Comparator时默认为最小堆），通过传入自定义的Comparator函数可以实现大顶堆。

```
PriorityQueue minHeap = new PriorityQueue(); //小顶堆，默认容量为11
PriorityQueue maxHeap = new PriorityQueue<Integer>(new Comparator<Integer>() { 
    @Override																	//大顶堆，默认容量为11
    public int compare(Integer o1, Integer o2) {
      /**以下是对比较器升序、降序的理解.
      *(1) 写成return o1.compareTo(o2) 或者 return o1-o2表示升序
      *(2) 写成return o2.compareTo(o1) 或者return o2-o1表示降序
      */
      return o2.compareTo(o1);
    }

}) ;
```

 

　　案例：[ 剑指offer(41) 最小的k个数](https://www.cnblogs.com/yongh/p/9944993.html)

PriorityQueue的常用方法有：poll(),offer(Object),size(),peek()等。

- 　　插入方法（offer()、poll()、remove() 、add() 方法）时间复杂度为O(log(n)) ；
- 　　remove(Object) 和 contains(Object) 时间复杂度为O(n)；
- 　　检索方法（peek、element 和 size）时间复杂度为常量。

 

 **PriorityQueue的API文档说明：**

| 构造方法摘要                                                 |
| ------------------------------------------------------------ |
| `**PriorityQueue**()`      使用默认的初始容量（11）创建一个 `PriorityQueue`，并根据其自然顺序对元素进行排序。 |
| `**PriorityQueue**(Collection c)`      创建包含指定 collection 中元素的 `PriorityQueue`。 |
| `**PriorityQueue**(int initialCapacity)`      使用指定的初始容量创建一个 `PriorityQueue`，并根据其自然顺序对元素进行排序。 |
| `**PriorityQueue**(int initialCapacity, Comparator comparator)`      使用指定的初始容量创建一个 `PriorityQueue`，并根据指定的比较器对元素进行排序。 |
| `**PriorityQueue**(PriorityQueue c)`      创建包含指定优先级队列元素的 `PriorityQueue`。 |
| `**PriorityQueue**(SortedSet c)`      创建包含指定有序 set 元素的 `PriorityQueue`。 |

 

| 方法摘要      |                                                              |
| ------------- | ------------------------------------------------------------ |
| ` boolean`    | `**add**(E e)`      将指定的元素插入此优先级队列。           |
| ` void`       | `**clear**()`      从此优先级队列中移除所有元素。            |
| ` Comparator` | `**comparator**()`      返回用来对此队列中的元素进行排序的比较器；如果此队列根据其元素的自然顺序进行排序，则返回 `null`。 |
| ` boolean`    | `**contains**(Object o)`      如果此队列包含指定的元素，则返回 `true`。 |
| ` Iterator`   | `**iterator**()`      返回在此队列中的元素上进行迭代的迭代器。 |
| ` boolean`    | `**offer**(E e)`      将指定的元素插入此优先级队列。         |
| ` E`          | `**peek**()`      获取但不移除此队列的头；如果此队列为空，则返回 `null`。 |
| ` E`          | `**poll**()`      获取并移除此队列的头，如果此队列为空，则返回 `null`。 |
| ` boolean`    | `**remove**(Object o)`      从此队列中移除指定元素的单个实例（如果存在）。 |
| ` int`        | `**size**()`      返回此 collection 中的元素数。             |
| ` Object[]`   | `**toArray**()`      返回一个包含此队列所有元素的数组。      |
| ` T[]`        | `**toArray**(T[] a)`      返回一个包含此队列所有元素的数组；返回数组的运行时类型是指定数组的类型。 |



| **从类 java.util.AbstractQueue 继承的方法** |
| ------------------------------------------- |
| `addAll, element, remove`                   |



| **从类 java.util.AbstractCollection 继承的方法**       |
| ------------------------------------------------------ |
| `containsAll, isEmpty, removeAll, retainAll, toString` |



| **从类 java.lang.Object 继承的方法**                         |
| ------------------------------------------------------------ |
| `clone, equals, finalize, getClass, hashCode, notify, notifyAll, wait, wait, wait` |

 

| **从接口 java.util.Collection 继承的方法**                   |
| ------------------------------------------------------------ |
| `containsAll, equals, hashCode, isEmpty, removeAll, retainAll` |