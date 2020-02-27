# 把对象添加至JsonObject和JsonArray中

> ### Student类

------

```java
package json;

public class Student {
    private String name;
    private int age;
    private String sex;

    public Student(String name, int age, String sex) {
        super();
        this.name = name;
        this.age = age;
        this.sex = sex;
    }

    public Student() {
        super();
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

}
```

> ### 测试用例

------

```java
package json;

import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;

/**
 * 使用TestNg进行测试
 * 
 * @author jarworker
 *
 */
public class TestJson {
    @BeforeClass
    public void beforeTest() throws Exception {
        System.out.println("快乐得测试代码！！！");
    }

    @Test
    public void testJsonObj() throws Exception {
        JSONObject jsonObj = new JSONObject();
        Student student_0 = new Student("jarworker", 18, "男");
        jsonObj.put("success", "123");
        jsonObj.put("student", student_0);
        System.out.println("添加对象到json对象:" + jsonObj.toJSONString());
        System.out.println("===============================================");
        JSONArray jsonArr = new JSONArray();
        Student student_1 = new Student("静香", 12, "女");
        Student student_2 = new Student("大熊", 13, "男");
        jsonArr.add(student_0);
        jsonArr.add(student_1);
        jsonArr.add(student_2);
        jsonObj.put("studentArr", jsonArr);
        System.out.println("添加对象到json数组:" + jsonObj.toJSONString());
        System.out.println("===============================================");
        System.out.println("对象中key为student的对象的name值为：" + jsonObj.getJSONObject("student").getString("name"));
    }

    @AfterTest
    public void afterTest() throws Exception {
        System.out.println("快乐得结束！！！");
    }
}
```

> ### **Console:输出**

------

```csharp
[TestNG] Running:
  C:\Users\huangkezhang\AppData\Local\Temp\testng-eclipse-1134102018\testng-customsuite.xml

快乐得测试代码！！！
添加对象到json对象:{"student":{"age":18,"name":"jarworker","sex":"男"},"success":"123"}
===============================================
添加对象到json数组:{"studentArr":[{"age":18,"name":"jarworker","sex":"男"},{"age":12,"name":"静香","sex":"女"},{"age":13,"name":"大熊","sex":"男"}],"student":{"$ref":"$.studentArr[0]"},"success":"123"}
===============================================
对象中key为student的对象的name值为：jarworker
快乐得结束！！！
PASSED: testJsonObj

===============================================
    Default test
    Tests run: 1, Failures: 0, Skips: 0
===============================================


===============================================
Default suite
Total tests run: 1, Failures: 0, Skips: 0
===============================================

[TestNG] Time taken by org.testng.reporters.jq.Main@626b2d4a: 94 ms
[TestNG] Time taken by [FailedReporter passed=0 failed=0 skipped=0]: 0 ms
[TestNG] Time taken by org.testng.reporters.JUnitReportReporter@123772c4: 14 ms
[TestNG] Time taken by org.testng.reporters.SuiteHTMLReporter@6f2b958e: 63 ms
[TestNG] Time taken by org.testng.reporters.XMLReporter@4361bd48: 7 ms
[TestNG] Time taken by org.testng.reporters.EmailableReporter2@41a4555e: 6 ms
```