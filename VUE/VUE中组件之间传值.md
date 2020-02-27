VUE中组件之间传值，总结来讲有三种情况，分别是：父组件对子组件、子组件对父组件以及兄弟组件之间传值以及调用。
一、父组件==>子组件
1.父组件传值给子组件，通过类似于属性绑定的方式，将需要传入子组件中的数据，绑定在子组件上，子组件通过props接收传入进来的数据。

父组件中内容
1
//在teamplate中调用此组件
<spList :keyword="keyword" :activename="active"></spList>
//引入子组件
import spList from "../../components/sp_list.vue";
components: {
    spList
},
data() {
    return {
        active: "2",
        keyword: '',
    };
},

子组件中内容
1
props: {
     keyword:String,
     activename:String,
},
//或者
props: {
     "keyword",
     "activename"
},

2.父组件调用子组件中的方法或数据，VUE官网中的描述：ref 被用来给元素或子组件注册引用信息。引用信息将会注册在父组件的 $refs 对象上。如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例。

父组件中内容
1
//在teamplate中调用此组件，并将该组件注册在$refs对象上
<spList ref="splist"></spList>
//引入子组件
import spList from "../../components/sp_list.vue";
components: {
    spList
},
methods: {
    getsomeList(){
        this.$refs.splist.getlist();//调用子组件中的方法
        this.$refs.splist.tableData;//获取子组件中的数据
    }
},
子组件中内容
1
data() {
    return {
        tableData:[],
    }
},
 methods: {
    //获取列表的方法
    getlist(){

    },
},

二、子组件==>父组件
1.通过事件派发的方式传值给父组件，或者告知父组件需要调用方法。

父组件中内容
1
//在teamplate中调用此组件，并绑定与子组件约定好的事件名称和在父组件中由该事件出发的方法
<spList @changeBxd="setBxd"></spList>
//引入子组件
import spList from "../../components/sp_list.vue";
components: {
    spList
},
methods: {
    setBxd(val){
        console.log(val);//'你好世界'
        this.getFlow();//触发事件后调用其他父组件中的方法
    },
    getFlow(){

    },
},

子组件中内容
1
methods: {
    //获取列表的方法
    getlist(){
        let name = '你好世界';
        this.$emit('changeBxd',name );//触发约定好的事件
    },
},

三、兄弟组件之间
1.通过eventbus的方式监听事件。
首先需要先创建一个eventbus的事件容器，哪里需要哪里引用。

> 兄弟组件1中的内容

```javascript
//引入eventbus
import Bus from '@/util/bus.js'
//在方法中触发事件，（提前约定好事件名称）
methods: {
    getFlow(){
        Bus.$emit('getCwbxList')
    },
},
```

> 兄弟组件2中的内容

```javascript
// 引入eventbus
import Bus from '@/util/bus.js'
mounted(){
    // 监听此事件
    Bus.$on('getCwbxList',()=>{
        this.getlist();
    })
}
```

> 注意：：eventbus 这种传值方式，适用于任何组件之间传值，父子间或者兄弟间。

另外，除了这些方法之外，还可以是用vuex官方推荐的状态管理。关于vuex在之后记录介绍，最近还在整理中。


原文链接：https://blog.csdn.net/airdark_long/article/details/81736889