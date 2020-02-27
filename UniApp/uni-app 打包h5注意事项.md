# uni-app 跨域以及打包h5注意事项

```javascript
"h5" : {
        "router" : {
            "mode" : "hash"
        },
        //配置好这个后，以后打包就会生产（./xxx）的引用，这样就可以通过浏览器直接打开而不需要架设成一个服务。但是需要注意的是，
        //当采用src引用时需要写出相对路径即（../../static/xxx.png），但是这样打包后是找不到该图片的，最好通过变量和require('../../static/img/java_05.png') 读取图片。（目前测试无效）
        // "publicPath" : "./",   //暂不采用
        "devServer" : {
            "port" : 8091,
            "disableHostCheck" : true,
            "proxy" : {  //用于反向代理，解决跨域问题
                "/api" : {
                    "target" : "http://localhost:38080",
                    // "target" : "http://140.143.23.199:38080",
                    "changeOrigin" : true,
                    "ws" : true,
                    "pathRewrite" : {
                        "^/api" : "/"
                    }
                }
            }
        },
        "title" : "IoT"
    }
```

实际请求场景

```javascript
//直接这样请求就可以了 不需要额外添加baseUrl
uni.request({
        url: '/api/iot/devices/locations', //仅为示例，并非真实接口地址。
        data: {
        },
        header: {
          'Blade-Auth': 'bearer '+ res.data.data.accessToken //自定义请求头信息
        },
        success: (res) => {
          console.log(res.data);
          // this.text = 'request success';
          // uni.$emit('deviceData',res.data)
          this.deviceData = res.data
          this.locationData = res.data
        }
 });
```



- 完整案例

```javascript
"h5": {
        "title": "FirstApp",
        "domain": "",
        "devServer": {
            /**
             * Vue跨域匹配的原理：
             第一步：把/api/v1中的第一个/替换成target
             如：target=http://127.0.0.1:8099 匹配结果：http://127.0.0.1:8099/api/v1
             如：target=http://127.0.0.1:8099/api2/v2 匹配结果为：http://127.0.0.1:8099/api2/v2/api/v1
             第二步：跨域之后再使用路径重写属性pathRewrite【转换成跨域路径后的结果再重写】
             如：配置一："^/api": "/api/v2"
                等价于http://127.0.0.1:8099/api/v1 会重写成 http://127.0.0.1:8099/api2/v2/v1
             **/
            "proxy": {
                "/api/v1": {
                    //你要跨域的域名(包含host、端口号,切记：一定要带上http头);
                    //同一个域名只能设置一次跨域，否则重复报错！
                    "target": "http://127.0.0.1:8099",
                    "changeOrigin": true //是否跨域，设置为true;(必须)
 
                    // 会把【跨域转向的路径】的/api开头的路径替换成:http://127.0.0.1:8099/api2/v2
                    // "pathRewrite": {
                    //     "^/api": "/api2/v2" // 设置/api开头路径重写成/api2/v2
                    // }
                }
            },
    }
```

