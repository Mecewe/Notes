#

#Mybaties——持久层框架

##  一、前述

### 1.1 mybatis概要

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191214170314457.png" alt="image-20191214170314457" style="zoom:40%;" />

Mybaties架构

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191030211409556.png" alt="image-20191030211409556" style="zoom:33%;" />

​									<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191030211604618.png" alt="image-20191030211604618" style="zoom:33%;"/> 

### 1.2 hibernate框架

![image-20191214164648950](/Users/mecewe/Library/Application Support/typora-user-images/image-20191214164648950.png)

### 1.3 mybatis框架

mybatis框架：半自动、轻量级的框架

![image-20191214170047804](/Users/mecewe/Library/Application Support/typora-user-images/image-20191214170047804.png)

## 二、映射文件

### 2.1 参数处理（单个参数、多个参数和命名参数）

![image-20191218220139695](/Users/mecewe/Library/Application Support/typora-user-images/image-20191218220139695.png)

![image-20191218220310140](/Users/mecewe/Library/Application Support/typora-user-images/image-20191218220310140.png)

![image-20191218220923651](/Users/mecewe/Library/Application Support/typora-user-images/image-20191218220923651.png)

![image-20191218220959798](/Users/mecewe/Library/Application Support/typora-user-images/image-20191218220959798.png)

- 实例

![image-20191218221412826](/Users/mecewe/Library/Application Support/typora-user-images/image-20191218221412826.png)

### 2.2 源码解析

![image-20191218224249013](/Users/mecewe/Library/Application Support/typora-user-images/image-20191218224249013.png)

### 2.3 #{ }和${ }区别

![image-20191219215415296](/Users/mecewe/Library/Application Support/typora-user-images/image-20191219215415296.png)

**大多数情况取参数的值应该使用#{ }**

![image-20191219215612875](/Users/mecewe/Library/Application Support/typora-user-images/image-20191219215612875.png)

###  2.4 #{ }更多用法

![image-20191219220025458](/Users/mecewe/Library/Application Support/typora-user-images/image-20191219220025458.png)

![image-20191219220136209](/Users/mecewe/Library/Application Support/typora-user-images/image-20191219220136209.png)

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191219215757690.png" alt="image-20191219215757690" style="zoom:43%;" />

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191219215832085.png" alt="image-20191219215832085" style="zoom:43%;" />

### 2.5 select查询

- method

![image-20191219221138566](/Users/mecewe/Library/Application Support/typora-user-images/image-20191219221138566.png)

- mapper

![image-20191219221219715](/Users/mecewe/Library/Application Support/typora-user-images/image-20191219221219715.png)

#### 自动映射

##### （1）我全局设置自动设置

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191219221445981.png" alt="image-20191219221445981" style="zoom:33%;" />

##### （2）自定义resultMap，实现高级结果集映射

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191220155518789.png" alt="image-20191220155518789" style="zoom:40%;" />

- ###### 联合查询：级联属性封装结果集

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191220161122794.png" alt="image-20191220161122794" style="zoom:33%;" />

- 使用**association**定义关联的单个对象的封装规则

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191220161042729.png" alt="image-20191220161042729" style="zoom:33%;" />

​			**懒加载开启 需要用的时候才查询**

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191220162754465.png" alt="image-20191220162754465" style="zoom:33%;" />

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191220163336592.png" alt="image-20191220163336592" style="zoom:33%;" />

- **collection**嵌套结果集的方式，定义关联的的集合类型元素的封装规则

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191220165019898.png" alt="image-20191220165019898" style="zoom:33%;" />

​			拓展

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221205136594.png" alt="image-20191221205136594" style="zoom:33%;" />

- **discriminator鉴别器**

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221205656984.png" alt="image-20191221205656984" style="zoom:33%;" />

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221205933684.png" alt="image-20191221205933684" style="zoom:33%;" />

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221205837140.png" alt="image-20191221205837140" style="zoom:33%;" />

### 2.6 动态SQL

#### （1）标签

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221210235600.png" alt="image-20191221210235600" style="zoom:33%;" />

#### （2）if

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221212005485.png" alt="image-20191221212005485" style="zoom:43%;" />

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221212656371.png" alt="image-20191221212656371" style="zoom:50%;" />

#### 	（3）trim

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221213020174.png" alt="image-20191221213020174" style="zoom:40%;" />

<img src="/Users/mecewe/Library/Application Support/typora-user-images/image-20191221213617578.png" alt="image-20191221213617578" style="zoom:40%;" />