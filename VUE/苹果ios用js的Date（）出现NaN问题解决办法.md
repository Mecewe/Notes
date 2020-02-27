###苹果ios用js的Date（）出现NaN问题解决办法

ios使用如下方法获得NaN，安卓手机则是正常计算，解决方法是换个这个时间的格式

```javascript
new Date("2017-04-28 23:59:59").getTime()//显示NaN  //.getTime()非常重要
//换成如下方式就正常了，就是‘-’换成‘/’
new Date("2017/04/28 23:59:59").getTime()//正确显示
```

###js时间相减函数苹果版相减为NAN（计算小时）

这个是安卓苹果通用的（计算小时）

```javascript
//两个日期的差值(d1 - d2).
function DateDiff(d1,d2){
    var day = 24 * 60 * 60 *1000;
    try{    
      if("ios" == api.systemType){
          d1 = d1.replace(' ','T');
          d2 = d2.replace(' ','T');
      }
   var checkTime = new Date(d1).getTime();
   var checkTime2 = new Date(d2).getTime();
   var cha = (checkTime - checkTime2)/day;  
        return cha;
    }catch(e){
   return false;
}
}//end fun
```



将如下2018-07-28 23:59:59改成2018/07/28 23:59:59

```javascript
var time='2018-11-21 12:01:22';
var time1=time.replace(/-/g,"/");//2018/11/21 12:01:22
```



