# 在vue中，localStorage本地存储应用

1、先存在localStorage里面。

localStorage.setItem('indexUrl','#/IndexA');

2、在用到的时候，获取数据

//获取本地
this.indexUrl = localStorage.getItem('indexUrl');

