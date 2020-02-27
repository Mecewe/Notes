## Scanner和BufferReader

###常规方法

#### 读取整数数组

**Scanner**(效率慢)

> 使用[`Scanner`](http://download.oracle.com/javase/6/docs/api/java/util/Scanner.html)[`Scanner.nextInt()`](http://download.oracle.com/javase/6/docs/api/java/util/Scanner.html#nextInt())

```java
Scanner s = new Scanner(new File("input.txt"));
int[] array = new int[s.nextInt()];
for (int i = 0; i < array.length; i++)
    array[i] = s.nextInt();
```

**BufferReader**（对于多值int解析复杂）

```java
BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
int n = Integer.valueOf(bf.readLine());
char[] arr = bf.readLine().trim().replace(" ","").toCharArray();
...
bf.close();
```

###加快Java的运行

[ACM之Java输入输出 - samjustin的博客 - 博客频道 - CSDN.NET](https://link.zhihu.com/?target=http%3A//blog.csdn.net/samjustin1/article/details/52087061)**有用**

[Faster Input for Java](https://link.zhihu.com/?target=https%3A//www.cpe.ku.ac.th/~jim/java-io.html)

**复用的代码**

```java
/** Class for buffered reading int and double values */
class Reader {
    static BufferedReader reader;
    static StringTokenizer tokenizer;

    /** call this method to initialize reader for InputStream */
    static void init(InputStream input) {
        reader = new BufferedReader(
                     new InputStreamReader(input) );
        tokenizer = new StringTokenizer("");
    }

    /** get next word */
    static String next() throws IOException {
        while ( ! tokenizer.hasMoreTokens() ) {
            //TODO add check for eof if necessary
            tokenizer = new StringTokenizer(
                   reader.readLine() );
        }
        return tokenizer.nextToken();
    }

    static int nextInt() throws IOException {
        return Integer.parseInt( next() );
    }
	
    static double nextDouble() throws IOException {
        return Double.parseDouble( next() );
    }
}
```

**适用例子**

```java
Reader.init( System.in ); // connect Reader to an input stream
double x = Reader.nextDouble();
int n = Reader.nextInt();
```



