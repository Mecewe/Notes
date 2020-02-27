###JDBC

> 连接池

提升性能；

> DBUtils

节省代码；

![image-20191015163526653](/Users/mecewe/Library/Application Support/typora-user-images/image-20191015163526653.png)

```java
try {
    QueryRunner queryRunner = new QueryRunner(C3P0Utils.getDataSouce());
    String sql = "insert into zhangwu values(null,?,?)";
    Object[] params = {"晚饭",235};
    int rows = queryRunner.update(sql,params);
    if(rows > 0){
        System.out.println("添加成功");
    }else {
        System.out.println("添加失败");
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

