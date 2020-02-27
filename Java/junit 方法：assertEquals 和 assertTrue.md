##junit 方法：assertEquals 和 assertTrue

assertEquals 和 assertTrue 区别

> 相同之处：都能判断两个值是否相等
> assertTrue 如果为true，则运行success，反之Failure
> assertEquals 如果预期值与真实值相等，则运行success，反之Failure

不同之处：

> assertEquals 运行Failure会有错误提示，提示预期值是xxx，而实际值是xxx，容易调式。
> assertTrue 没有错误提示

####代码块

**App.java**

```java
package com.yubai.Test;

public class App 
{
    public String method(){
        return this.getClass().getName();
    }
}
```

**AppTest.java**

```java
package com.yubai.Test;

import static org.junit.Assert.*;//必须是static
import org.junit.Test;

public class AppTest {
    App app = new App();
    @Test
    public void testBaseClass(){
     assertTrue(app.method().equals("com.yubai.Test.App"));
    }

    @Test
    public void testmethod(){
        assertEquals("com.yubai.Test.App", app.method());
    }
}
```

