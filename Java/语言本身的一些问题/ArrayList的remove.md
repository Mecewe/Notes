## 关于ArrayList的remove方法问题

#### List.remove()有两个，一个`public E remove(int index)`，一个是`public boolean remove(Object o)`

```java
    public static void main(String[] args) {
      
        ArrayList<Integer> integers = new ArrayList<>();
        integers.add(1);
        integers.add(2);
        integers.add(3);
        integers.add(4);

        System.out.println(integers);
        integers.remove(1);   //[1, 3, 4]
//        integers.remove((Integer) 1);   //[2, 3, 4]
        System.out.println(integers);
    }
```

 基于这种设想的原因是，既然ArrayList<Integer>里的类型是Integer，我传入一个int的应该可以**自动实现autoboxing**.那么，

实际运行的结果不然：

Exception in thread "main" java.lang.IndexOutOfBoundsException: Index: 25, Size: 20

​	at java.util.ArrayList.rangeCheck(ArrayList.java:604)

​	at java.util.ArrayList.remove(ArrayList.java:445)

​	at CollectionBasics.main(CollectionBasics.java:54)

**事实是**由于有多态的**remove()**方法，为了移除制定的元素而不至于引起混淆的话，可以将传入的int先封装一下：

`integers.remove((Integer) 1)`

