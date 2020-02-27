###js中如何将字符串转化为时间，并计算时间差

ios时间可能不能识别yyyy-MM-dd hh24:mi:ss格式

```javascript
//结束时间  
end_str = ("2014-01-01 10:15:00").replace(/-/g,"/");//一般得到的时间的格式都是：yyyy-MM-dd hh24:mi:ss，所以我就用了这个做例子，是/的格式，就不用replace了。  
var end_date = new Date(end_str);//将字符串转化为时间  
//开始时间  
sta_str = ("2014-01-01 10:15:00").replace(/-/g,"/");  
var sta_date = new Date(sta_str);  
var num = (end_date-sta_date)/(1000*3600*24);//求出两个时间的时间差，这个是天数  
var days = parseInt(Math.ceil(num));//转化为整天（小于零的话剧不用转了）  

//下面才附上js中一些针对时间类操作的方法  
var myDate = new Date();    
myDate.getYear();      //获取当前年份(2位)    
myDate.getFullYear(); //获取完整的年份(4位,1970-????)    
myDate.getMonth();      //获取当前月份(0-11,0代表1月)    
myDate.getDate();      //获取当前日(1-31)    
myDate.getDay();        //获取当前星期X(0-6,0代表星期天)    
myDate.getTime();      //获取当前时间(从1970.1.1开始的毫秒数)    
myDate.getHours();      //获取当前小时数(0-23)    
myDate.getMinutes();    //获取当前分钟数(0-59)    
myDate.getSeconds();    //获取当前秒数(0-59)    
myDate.getMilliseconds(); //获取当前毫秒数(0-999)    
myDate.toLocaleDateString();    //获取当前日期    
var mytime=myDate.toLocaleTimeString();    //获取当前时间    
myDate.toLocaleString( );   //获取日期与时间----如果涉及到时分秒，直接使用即可。   
```

