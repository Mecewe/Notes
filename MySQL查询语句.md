## MySQL查询语句

###常规顺序

``````mysql
select count(*)
from product
where
group by cid
having
order by
``````

![image-20191007211337613](/Users/mecewe/Library/Application Support/typora-user-images/image-20191007211337613.png)

####查询最新10条数据方法

```
select * from 表名 order by id（主键） desc limit 10
```

