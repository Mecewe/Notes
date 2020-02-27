# Java数组类型

> https://www.jianshu.com/p/d9c0e0f07fda

#### 数组类型和数组引用变量详解

> 数组类型
>
> 为什么要用数组？
>
> Java数组的两大特征：
>
> 定义数组时，不能指定数组的长度
>
> 变量分为 2 种：
>
> 数组的初始化：
>
> 遍历数组：
>
> 深入理解数组的存放：
>
> 二维数组与多维数组
>
> Arrays工具类，提供一些方法来操作数组。



## 数组类型  

Java 数据类型可以分为：基本类型 — 8 个

​                     引用类型 — 类、接口、数组

数组是引用类型。

int → int [ ]  — 整型数组

double → double [ ]  — double 数组

……

String → String [ ]  — String 数组

int [ ] → int [ ] [ ]    — 新的数组类型

int [ ] [ ] → int [ ] [ ] [ ]    — 新的数组类型

PS:

  // 类型 变量名

int a [ ];       // 垃圾写法，虽然正确，但是可读性差

  // 类型是 int [ ] ，变量名是 a

int [ ] a;       // 正确写法

 **数组类型**：**就是一个真正的类型，它即可用于创建变量，也可用于进行强制类型转换**

## 为什么要用数组？  

如果程序中需要用到多个相同类型的变量，就可以考虑把它们集中定义成一个数组。

——每个数组元素，就相当于一个普通的变量

借助于数组，我们可以非常方便地去管理、访问每个数组元素（相当于一个变量）

## Java数组的两大特征：

​    Java语言是强类型： 一个数组里只能存储一种数据类型的数据
​    Java语言是静态的： Java的数组一旦被初始化之后，它的长度是固定的。

## 定义数组时，不能指定数组的长度

数组类型是引用类型。

引用类型的本质就是指针。——指针也是变量，只不过它里面存的值是内存编号（内存地址）

数组变量只是一个引用，因此声明时只是定义了一个引用变量，并未真正指向有效的数组对象（存在），也就是并未真正指向有效的内存，因此不能声明长度，而且也不能使用。

### 变量分为 2 种：

  1.直接在变量中存放实际的变量值。这就是Java的基本类型的变量。

  2.在变量中存放只是内存的地址值，这就是所谓的引用变量。

## 数组的初始化：

  数组变量只是一个引用，必须让它指向有效的内存之后才能使用

初始化分为两种：

####   静态初始化：

​    new <type> [ ] {<ele1>,<ele2>,<ele3>...};   // <>里可替换

​    只指定数组的元素，让系统来决定数组的长度。

####   动态初始化：

​    new <type> [ <length> ]       // <>里可替换

​    只指定数组的长度，让系统来决定数组的元素的值。

如果数组元素是基本类型，那么所有数组元素的值都是 0 / 0.0 / false / \u0000 （只记都是零）

如果数组元素是引用类型，那么所有数组元素的值都是 null

一旦数组的初始化完成，接下来的每个数组元素就可当成普通变量使用了。

#### 使用数组：  

每个数组元素相当于一个变量，该变量的类型，就是数组类型去掉【一个】方括号。

数组有一个 length 属性，用于返回该数组的长度。

#### 遍历数组：

  A. 可以依次根据每个数组元素的索引来进行遍历。

  B. 使用 foreach 循环进行遍历。

for（数组或集合元素的类型 变量名：数组\集合）

{

   // 此处即可通过”变量名“依次访问每个数组\集合的元素

}

注意点：foreach 循环时，不要对循环变量赋值！

********如果要在遍历时对数组元素进行赋值，那就应该根据数组元素的索引来进行遍历

/****************************************************

补充：

\1. 内存泄露：c语言，把内存分配出去之后，后面忘记了回收这些内存

\2. 对象还存在，以后还要用的时候，内存早早就把对象清理出去了

***********************************************************/

Java 就把指针换个名字，叫引用。

​    对指针做了一些包装、做了一些检查——这样可以保证引用更加安全

​    引用：被包装后的、更加安全的引用

/*********************************************************

补充：

JVM有一条后台进程：垃圾回收器

​    它会用一种机制记录 堆内存 中“每个对象”是否有引用变量（指针）引用它

​       如果有，垃圾回收器就不会管它。

​      如果没有，垃圾回收器就会在合适时候去回收该对象所占的内存

*********************************************************/

#### 深入理解数组的存放：  

​    当数组对象的引用变量被销毁之后，数组对象并不一定会被回收（它在堆内存），它不会随着数组变量被回收。

​    只有当没有引用变量引用这个数组对象时，系统才会去回收数组对象。

![img](https://upload-images.jianshu.io/upload_images/6171290-b3b5eeefe8d61ac0.png?imageMogr2/auto-orient/strip|imageView2/2/w/570/format/webp)

方法栈堆内存

***PriArrayTest 程序 及 运行结果：***

public class PriArrayTest

{

  public static void main(String[] args)

  {

​    // 所有在方法里声明的变量，都放在对应的方法栈。

​    /*

​     \* 每个方法运行时，系统都会为之建立一个方法栈

​     \* 栈内存是临时性的内存，当方法结束时，方法栈会被立即释放

​     \* 所以栈内存不适合存放长期有效的数据

​     *

​     \* 堆内存：每个JVM 只有一个

​     \*     只要JVM不退出，堆内存将一直存在

​    */ 

​     double d = 23.5; // d 是基本类型

​     int[] iarr = null; // 它只是数组变量，引用变量。

​               // 此时这个iarr不能使用。

  // NullPointerException异常，空指针异常

  // 当程序访问一个 null 对象的实例方法或实例属性

  // 程序就会引发NullPointerException异常

  //	System.out.println(iarr[0]);

​    iarr = new int[4]; // 所有的对象都放在“堆”内存

  // 每个JVM（虚拟机）只有一个“堆”内存

  // 在Java程序里，只要访问“引用”的方法、属性时，

  // 系统会自动切换到访问它实际的对象

  // 堆内存中的对象，只能通过引用变量来访问

​     iarr[2] = 34; // 34是基本类型，但它实际上存在“堆内存”中

​     System.out.println(iarr.length);

  // 静态初始化的简化语法

​     int[] ba = {12,20,102};

​     iarr = ba; // 把ba的值赋给iarr

​    System.out.println(iarr.length);

  }

}

![img](https:////upload-images.jianshu.io/upload_images/6171290-65e82b9c93e8990a.png?imageMogr2/auto-orient/strip|imageView2/2/w/565/format/webp)

iarr=ba 根本原因
 

此时 0x12ab34ed 没有被引用，垃圾回收器会在合适的时候回收它



***数组测试 程序 及 运行结果：*** 

public class 数组测试

{

  public static void main(String[] args)

  {

  int[] iArr;  // 声明了一个数组变量。引用类型变量（基础就那8个）。它存放的是内存变量

  // iArr 是一个引用类型的变量

  // 也就是 iArr 存放了后面创建的数组的地址。

// 静态初始化

  iArr = new int[]{20,1,12,32};

  System.out.println(iArr[0]);

  iArr[0] = 'A';// 'A'本来是 char，但由 char 可以自动转换 int 类型

  System.out.println(iArr[0]);

// 动态初始化

  String[] strArr = new String[5];

  // 第一个数组元素的索引是 0

  // 最后一个数组元素的索引是 length - 1

  // 把数组的最后一个元素赋值为 "明天就周六啦~~~"

  strArr[strArr.length - 1] = "明天就周六啦~~~";

  // 遍历数组元素

  for(int i = 0;i < strArr.length;i++)

  {

​    System.out.println("strArr[" + i + "]: " + strArr[i]);

  }

  // 当我们访问数组元素的 索引小于0 ，或者大于等于length

  // 将引发“数组索引越界”异常

  System.out.println(strArr[strArr.length]);

  }

}

![img](https:////upload-images.jianshu.io/upload_images/6171290-3b2f19ef1f99a6ae.png?imageMogr2/auto-orient/strip|imageView2/2/w/590/format/webp)

数组测试

# 二维数组与多维数组  

#### 所谓的“二维”数组  

int[ ]    →  int[ ] [ ]

int[ ][ ]  →  int[ ][ ][ ]

***MultiDimenTest (二维数组)程序 及 运行结果：***

public class MultiDimenTest***
***

{

  public static void main(String[] args)

  {

​     int[][] arr; // 只是一个引用变量。

​     // 动态初始化，由系统为数组元素赋值

​     arr = new int[4][]; // Java允许初始化数组时候只初始化左边的维数

​     System.out.println(arr[1]); // arr[1]相当于一个int[]变量

​     arr[1] = new int[]{12,15}; // 静态初始化语法创建数组对象。

  //	arr[1][2] = 30; // 此处赋值没有问题，[1][2] 是int型，但是会引发数组索引越界的异常

  //	arr[2][0] = 13; // 由于arr[2]相当于int[]类型的变量（即引用变量）

​               // 此时它还未指向有效的内存。因此会引发NullPointerException（空指针异常）

​     int[] a = new int[3]; // 动态初始化

​     arr[2] = a; // 把 a 变量存放的地址赋给arr[2]

​     a[2] = 102; // a是int型

​     for(int i = 0;i < arr[2].length;i++)

​     {

​       System.out.println("~~~~~" + arr[2][i]);

​       if(i == 1)

​       {

​         arr[2][i] = 23;

​       }

​     }

​     for(int i = 0;i < a.length;i++ )

​     {

​       System.out.println(a[i]);

​     }

  }

}

![img](https:////upload-images.jianshu.io/upload_images/6171290-fa7ebf05d7a38a7e.png?imageMogr2/auto-orient/strip|imageView2/2/w/503/format/webp)

MultiDimenTest内存结构 

####  

![img](https:////upload-images.jianshu.io/upload_images/6171290-a61fcbc688580e0a.png?imageMogr2/auto-orient/strip|imageView2/2/w/412/format/webp)

MultiDimenTest

#### 多维数组

三维数组的元素是二维数组

二维数组的元素是一位数组

N维数组的元素是N-1维数组（这话是不标准的，只是为了方便记忆）

***多维数组 程序 及 运行结果：***

public class 多维数组***
***

{

  public static void main(String[] args)

  {

​     int[][] a = new int[2][3];

​     System.out.println("a的长度：" + a.length);

​     a[1] = new int[]{13,23,10,45};

​     // a的length是2

​     for(int i = 0;i < a.length;i++)

​     {

​       for(int j = 0;j < a[i].length;j++)

​       {

​       System.out.print(a[i][j] + "\t");

​       }

​     System.out.print("\n");

​     }

  }

}

***
***



![img](https:////upload-images.jianshu.io/upload_images/6171290-9a84427ef37cd170.png?imageMogr2/auto-orient/strip|imageView2/2/w/502/format/webp)

原理



![img](https:////upload-images.jianshu.io/upload_images/6171290-dc33cb9c3db4a049.png?imageMogr2/auto-orient/strip|imageView2/2/w/482/format/webp)

结果
 

# Arrays工具类，提供一些方法来操作数组。  

binarySearch  —  二分法查找。用于查找数组中的元素。

​                但是，要求数组元素已经是排好序。

sort（char[ ] a) —  可用于对数组进行排序

fill (type [] a,  int fromIndex,  int toIndex,  type val)

  ( 类型，     开始的值 ，    结束的值   ，填充的值)

***Arrays工具类 程序 及 运行结果：***

import java.util.*;

// 只有java.lang 包的类不需要导入。

public class Arrays工具类

{

  public static void main(String[] args)

  {

  int[] a = new int[]{12,23,34,37,41,46,54,67};

  int index1 = Arrays.binarySearch(a,46);

  System.out.println(index1);

  int[] b = new int[]{12,46,23,34,37,41,54,67};

  int index2 = Arrays.binarySearch(b,46);

  System.out.println(index2);

  // 将b数组的从索引为1的元素到索引5之前的元素，都填充成20

  Arrays.fill(b,1,5,20);

  System.out.println(b); // 直接打印数组，看到[ 数组类型的首字母大写@地址值

  // Arrays 的tostring可以帮助你看到数组元素

  System.out.println(Arrays.toString(b));

  }

}



![img](https:////upload-images.jianshu.io/upload_images/6171290-36adc3d9b7804c6f.png?imageMogr2/auto-orient/strip|imageView2/2/w/476/format/webp)

Arrays工具类





练习：

把数字翻译成人名币的读法

例如： 10010202.12       壹仟零壹万两佰零贰圆壹角贰分

汉字定义成数组