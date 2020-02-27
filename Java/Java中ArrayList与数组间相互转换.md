[Java中ArrayList与数组间相互转换](https://www.cnblogs.com/bosongokay/p/6768468.html)

在实际的 Java 开发中，如何选择数据结构是一个非常重要的问题。

衡量标准化(读的效率与改的效率) ：

​    ① Array： 读快改慢

​    ② Linked ：改快读慢

​    ③ Hash：介于两者之间

**实现List、Set和数组之间转换的关键点如下：（一定要注意泛型的引用）**

 　1. List转换成数组可以使用List的toArray方法，返回一个Object数组；

 　  2. Set转换成数组可以使用Set的toArray方法，返回一个Object数组；

   \3. 如果List或Set中元素的类型都为A，那么可以使用带参数的toArray方法，得到类型为A的数组，具体语句是“（A[]）set.toArray(new A[0])”；

  　4. 数组转换成List可以使用Arrays的asList静态方法，得到一个List；

   \5. 数组转化成Set时，需要先将数组转化成List再用List构造Set；

 Demo_1：List 转数组

```
import java.util.*;public class Test {  public static void print(Double arr[]) {    for (int i=0; i      System.out.print(arr[i]+" ");    }    System.out.println();  }  public static void main(String[] args) {     ArrayList list = new ArrayList();    // 若不写成泛型()的方式，则下面： Double arr3[] = list.toArray(new Double[0]);    // 要改写成：Double arr3[] = (Double[])list.toArray(new Double[0]);    list.add(1.23);     list.add(4.57);     list.add(2.38);    list.add(4.598);    int size = list.size();    System.out.println(size); // 输出：4// 第一种方法，不推荐    Double arr1[] = new Double[size];    for(int i=0;i      arr1[i]=(double)list.get(i);     }     print(arr1); // 输出：1.23 4.57 2.38 4.598// 第二种方法，推荐    // 当list中的数据类型都一致时可以将list转化为数组    Object arr2[] = list.toArray();    System.out.println("从list转换成的对象数组长度为：" + arr2.length); // 输出：从list转换成的对象数组长度为：4    // 在转化为其它类型的数组时需要强制类型转换，并且，要使用带参数的toArray方法，参数为对象数组.    // 将list中的内容放入参数数组中，当参数数组的长度小于list的元素个数时，会自动扩充数组的长度以适应list的长度    Double arr3[] = list.toArray(new Double[0]);    System.out.println("从list转换成的字符串数组长度为：" + arr3.length); // 输出：从list转换成的字符串数组长度为：4    print(arr3); // 输出：1.23 4.57 2.38 4.598    // 分配一个长度与list的长度相等的字符串数组    Double[] arr4 = list.toArray(new Double[list.size()]);    System.out.println("从list转换成的字符串数组长度为：" + arr4.length); // 输出：从list转换成的字符串数组长度为：4    print(arr4); // 输出： 1.23 4.57 2.38 4.598  }}
```

 Demo_2：数组转 List

```
import java.util.*;public class Test {    public static void main(String[] args) {     List list = new ArrayList();     list.add(1.23);     list.add(4.57);     list.add(2.38);     list.add(4.598);     System.out.println(list); // 输出：[1.23, 4.57, 2.38, 4.598]     list.clear();     System.out.println(list.size()); // 输出：0    // 直接使用Arrays的asList方法     Double arr[] = {1.23,4.57,2.38,4.598};     list = Arrays.asList(arr);     System.out.println("将数组转换成list的元素个数为：" + list.size()); // 输出：将数组转换成list的元素个数为：4     System.out.println(list); // 输出：[1.23, 4.57, 2.38, 4.598]    }}
```

 Demo_3：set 转数组

```
import java.util.*;public class Test {  public static void print(Double arr[]) {    for (int i=0; i      System.out.print(arr[i]+" ");    }    System.out.println();  }  public static void main(String[] args) {     HashSet set = new HashSet();    // 若不写成泛型()的方式，则下面： Double arr3[] = set.toArray(new Double[0]);    // 要改写成：Double arr3[] = (Double[])set.toArray(new Double[0]);    set.add(1.23);     set.add(4.57);     set.add(2.38);    set.add(4.598);    int size = set.size();    System.out.println(size); // 输出：4// 第一种方法，不推荐    Double arr[] = new Double[size];    Iterator i = set.iterator();    // 若写成 Iterator i = set.iterator()，则下面要写成 arr[j] = (Double) i.next();    int j =0;    while(i.hasNext()){      arr[j] = i.next();      j++;    }    print(arr); // 输出：4.598 2.38 1.23 4.57// 第二种方法，推荐    // 当set中的数据类型都一致时可以将set转化为数组    Object arr1[] = set.toArray();    System.out.println("从set转换成的对象数组长度为：" + arr1.length); // 输出：从set转换成的对象数组长度为：4    // 在转化为其它类型的数组时需要强制类型转换，并且，要使用带参数的toArray方法，参数为对象数组.    // 将set中的内容放入参数数组中，当参数数组的长度小于set的元素个数时，会自动扩充数组的长度以适应list的长度    Double arr2[] = set.toArray(new Double[0]);    System.out.println("从set转换成的Double数组长度为：" + arr2.length); // 输出：从list转换成的字符串数组长度为：4    print(arr2); // 输出：4.598 2.38 1.23 4.57    // 分配一个长度与list的长度相等的字符串数组    Double[] arr3 = set.toArray(new Double[set.size()]);    System.out.println("从set转换成的字符串数组长度为：" + arr3.length); // 输出：从list转换成的字符串数组长度为：4    print(arr3); // 输出： 4.598 2.38 1.23 4.57  }}
```

 Demo_4：数组转 set

```
import java.util.*;public class Test {    public static void main(String[] args) {     HashSet set = new HashSet();     set.add(1.23);     set.add(4.57);     set.add(2.38);     set.add(4.598);     System.out.println(set); // 输出：[4.598, 2.38, 1.23, 4.57]     set.clear();     System.out.println(set.size()); // 输出：0     Double arr[] = {1.23,4.57,2.38,4.598};     // 间接使用Arrays的asList方法，将数组转换成List后，再用List构造Set     set = new HashSet(Arrays.asList(arr));     System.out.println("将数组转换成set的元素个数为：" + set.size()); // 输出：将数组转换成set的元素个数为：4     System.out.println(set); // 输出：[4.598, 2.38, 1.23, 4.57]    }}
```