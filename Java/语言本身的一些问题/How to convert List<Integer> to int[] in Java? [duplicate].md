# [How to convert List to int in Java? ](https://stackoverflow.com/questions/960431/how-to-convert-listinteger-to-int-in-java)

#### 方法一

I'm new to Java. How can i convert a `List` to `int[]` in Java? I'm confused because `List.toArray()` actually returns an `Object[]`, which can be cast to nether `Integer[]` or `int[]`.

Right now I'm using a loop to do so:

```
int[] toIntArray(List<Integer> list){
  int[] ret = new int[list.size()];
  for(int i = 0;i < ret.length;i++)
    ret[i] = list.get(i);
  return ret;
}
```

#### 方法二

No one mentioned yet streams added in Java 8 so here it goes:

```
int[] array = list.stream().mapToInt(i->i).toArray();
```