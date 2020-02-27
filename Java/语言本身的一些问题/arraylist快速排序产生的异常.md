## ArrayList排序产生的异常

#### 代码内容

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
         ArrayList<ListNode> nodeArray = new ArrayList<>();

        for (int i = 0; i < lists.length; i++) {
            ListNode head = lists[i];
            while (head != null) {
                nodeArray.add(head);
                head = head.next;
            }
        }
        if(nodeArray.size() == 0){
            return null;
        }
        Comparator comp = new comp();
//        Arrays.sort(nodeArray,new comp());
        // Collections.sort(nodeArray,comp); //可行
        nodeArray.sort(comp);								//可行
        for(int i = 1;i<nodeArray.size();i++){
            nodeArray.get(i-1).next = nodeArray.get(i);
        }
        nodeArray.get(nodeArray.size()-1).next = null;
        return nodeArray.get(0);
    }
    
    class comp implements Comparator<ListNode> {
        @Override
        public int compare(ListNode o1, ListNode o2) {
          if(o1 != null && o2!= null){
            if(o1.val < o2.val){
              return -1;
            }else if(o1.val == o2.val) {
              return 0;
            }else {
              return 1;
            }
          }else {
            return 0;
          }
          // return o1.val.compareTo(o2.val);
        }
    }
}
```

#### 异常

⚠️使用Comparator排序 jdk1.7 1.8容易抛出以下异常，需要满足以下**三个性质**！

`java.lang.IllegalArgumentException: Comparison method violates its general contract!`

> 在 JDK7 版本以上，Comparator 要满足**自反性**，**传递性**，**对称性**，不然 Arrays.sort，
>
>Collections.sort 会报 IllegalArgumentException 异常。
>
>说明：
>
>1） 自反性：x，y 的比较结果和 y，x 的比较结果相反。
>
>2） 传递性：x>y,y>z,则 x>z。
>
>3） 对称性：x=y,则 x,z 比较结果和 y，z 比较结果相同。

反例：下例中**没有处理相等**的情况，实际使用中可能会出现异常：

```java
new Comparator<Student>() {
    @Override
    public int compare(Student o1, Student o2) {
        //return o1.getId() > o2.getId() ? 1 : -1; //错误方式
        if(o1.getId() > o2.getId()){							//正确方式
          return 1;
        }else if (o1.getId() < o2.getId()){
          return -1;
        }else{
          return 0;
        }
    }
} 
```

# 分析

在我以前的认知中，高版本的JDK是可以兼容之前的代码的，与同事讨论了一番另加搜索了一番，事实证明，JDK6到JDK7确实存在兼容问题（[不兼容列表](http://www.oracle.com/technetwork/java/javase/compatibility-417013.html#incompatibilities)）。在不兼容列表中我们可以找到关于Collections.sort的不兼容说明，如下：

```
Area: API: Utilities
Synopsis: Updated sort behavior for Arrays and Collections may throw an IllegalArgumentException
Description: The sorting algorithm used by java.util.Arrays.sort and (indirectly) by java.util.Collections.sort has been replaced. 
The new sort implementation may throw an IllegalArgumentException if it detects a Comparable that violates the Comparable contract. 
The previous implementation silently ignored such a situation.
If the previous behavior is desired, you can use the new system property, java.util.Arrays.useLegacyMergeSort, 
to restore previous mergesort behavior.
Nature of Incompatibility: behavioral
RFE: 6804124
```

描述的意思是说，java.util.Arrays.sort(java.util.Collections.sort调用的也是此方法)方法中的排序算法在JDK7中已经被替换了。如果违法了比较的约束新的排序算法也许会抛出llegalArgumentException异常。JDK6中的实现则忽略了这种情况。那么比较的约束是什么呢？[看这里](http://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html#compare(T, T))，大体如下：

> ![img](http://img.blog.csdn.net/20141218224145015?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2hzYXU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

 

 

- sgn(compare(x, y)) == -sgn(compare(y, x))
- ((compare(x, y)>0) && (compare(y, z)>0)) implies compare(x, z)>0
- compare(x, y)==0 implies that sgn(compare(x, z))==sgn(compare(y, z)) for all z

再回过头来看我们开篇有问题的实现：

```
return x > y ? 1 : -1;
```

当x == y时，sgn(compare(x, y))  = -1，-sgn(compare(y, x)) = 1，这违背了sgn(compare(x, y)) == -sgn(compare(y, x))约束，所以在JDK7中抛出了本文标题的异常。

# 结论

那么现在是否可以盖棺定论了，按照上面的分析来看，使用这种比较方式（return x > y ? 1 : -1;），只要集合或数组中有相同的元素，就会抛出本文标题的异常。实则不然，什么情况下抛出异常，还取决于JDK7底层排序算法的实现，也就是大名鼎鼎的[TimSort](http://svn.python.org/projects/python/trunk/Objects/listsort.txt)。后面文章会分析TimSort。本文给出一个会引发该异常的Case，以便有心人共同研究，如下：

```
Integer[] array = 
{0, 0, 0, 0, 0, 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 2, 1, 0, 0, 0, 2, 30, 0, 3};
```

https://www.cnblogs.com/firstdream/p/7204067.html

