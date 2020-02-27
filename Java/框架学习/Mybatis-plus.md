#### 



### 一、通用CRUD

insert方法

插入时会根据每个属性进行非空判断，只有非空的属性对应的字段才会出现在SQL语句中

insertAllColumn方法

在插入时，不管属性是否非空，属性所对应的字段都会出现到SQL语句中

#### 1、插入操作

![image-20191224144126422](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224144126422.png)

#### 2、更新操作

![image-20191224145645367](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224145645367.png)

#### 3、查询操作

![image-20191224150633385](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224150633385.png)

#### 4、删除操作

![image-20191224152245441](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224152245441.png)

#### 5、MP启动注入原理分析

待定



### 二、条件构造器—Wrapper

![image-20191224182456950](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224182456950.png)

#### 1、带条件的查询

![image-20191224225100651](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224225100651.png)

#### 2、带条件的修改

![image-20191224225126971](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224225126971.png)

#### 3、带条件的删除

![image-20191224225149798](/Users/mecewe/Library/Application Support/typora-user-images/image-20191224225149798.png)