## uni-app跨域问题解决方法

跨域，就是A域名下的js，想请求B域名下的接口数据。
跨域，只存在于**浏览器端**。App和小程序不存在跨域问题。
跨域，分**浏览器策略**和**服务器策略**。



#### 跨域解决方法：

1、前端设置反向代理(用于调试) ，nginx设置好反向代理

例：[代码实例](/Users/mecewe/Documents/markdown/UniApp/uni-app 打包h5注意事项.md)

2、后端解决跨域问题

 ```java
import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
@WebFilter(filterName="CorsFilter",urlPatterns="/*")
public class CorsFilter implements Filter {

@Override
public void init(FilterConfig filterConfig) throws ServletException {

}

@Override
public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
    HttpServletResponse response = (HttpServletResponse) servletResponse;
    HttpServletRequest request = (HttpServletRequest)servletRequest;

    String origin = request.getHeader("Origin");
    response.setHeader("Access-Control-Allow-Origin", origin);
    response.setHeader("Access-Control-Allow-Methods", "POST, GET, OPTIONS, DELETE");
    response.setHeader("Access-Control-Max-Age", "3600");
    response.setHeader("Access-Control-Allow-Headers", "x-requested-with,Authorization");
    response.setHeader("Access-Control-Allow-Credentials", "true");
    String method = request.getMethod();
    if(method.equalsIgnoreCase("OPTIONS")){
        servletResponse.getOutputStream().write("Success".getBytes("utf-8"));
    }else{
        filterChain.doFilter(servletRequest, servletResponse);
    }
}

@Override
public void destroy() {

}
}
 ```



- 如果服务器配置了允许跨域，那就没有跨域问题
- 如果uni-app发布的H5页面和服务器接口部署在同一个域名下，那就没有跨域问题
- 如果服务器不能配跨域，开发期间为了调试方便，想让开发机的ip可以跨域访问服务器接口，那么可以在开发机chrome上安装一个跨域插件。详见下：



当我们使用谷歌浏览器调试ajax请求的时候可能会遇到这两个问题：

- 跨域资源共享 详见：[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- 跨源读取阻塞 详见：[CORB](https://www.chromestatus.com/feature/5629709824032768)

最常见的就是关于**跨域资源共享**的问题，也就是我们通常说的跨域。当我们本地服务器预览页面，使用ajax访问远程服务器的内容时就会请求失败，比如：本地预览的地址是：http://localhost:8080/，访问的接口地址是http://dcloud.io/api。

如果仅仅是为了本地预览，可以使用Chrome浏览器插件来协助调试。
**!!!** 本插件只能解决**简单请求**的跨域调试（[点击搜索什么是简单请求](https://www.baidu.com/s?wd=简单请求&tn=84053098_3_dg&ie=utf-8)）。对于非简单请求的OPTION预检（[点击搜索什么是预检请求](https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=1&tn=84053098_3_dg&wd=预检请求&oq=OPTION%E9%A2%84%E6%A3%80&rsv_pq=a0831c7c0000a93c&rsv_t=0313nBZdJJqdOJUR7zNSs%2BMXe8O6I0B9hizxu4eiVIV%2BBy5DUc%2FsouJj%2BQH2dyTBn%2BfLQg&rqlang=cn&rsv_enter=1&inputT=2653&rsv_sug3=3&rsv_sug1=2&rsv_sug7=100&rsv_sug2=1&prefixsug=%E9%A2%84%E6%A3%80&rsp=1&rsv_sug4=2654)）以及线上服务器也有跨域需求的用户，可以[服务端配合解决](https://www.baidu.com/s?wd=服务端跨域&tn=84053098_3_dg&ie=utf-8)。

## 插件名称：Allow-Control-Allow-Origin: *