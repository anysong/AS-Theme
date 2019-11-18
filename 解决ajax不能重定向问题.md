## 解决ajax不能重定向问题

### 背景
> 以前写response.sendRedirect("/login.jsp");是成功的，今天用到ajax请求，发送给后台，希望直接跳转，发现无效，
> 首先要深入了解ajax请求和response.sendRedirect的机制
#### response.sendRedirect的机制
> 这种方式是在客户端作的重定向处理。该方法通过修改HTTP协议的HEADER部分,对浏览器下达重定向指令的，让浏览器对在location中指定的URL提出请求，
> 使浏览器显示重定向网页的内容。该方法可以接受绝对的或相对的URLs。如果传递到该方法的参数是一个相对的URL，
> 那么Web container在将它发送到客户端前会把它转换成一个绝对的

首先需要确认XHR,JSONP,CORS

### XHR
原因: ajax 是默认就是不支持重定向的，它是局部刷新，不重新加载页面。  
解决: ajax请求可以用getResponseHeader获取头信息  
后端: 添加响应头
```bash
//告诉ajax我是重定向
response.setHeader("REDIRECT", "REDIRECT");
//告诉ajax我重定向的路径
response.setHeader("CONTENTPATH", basePath+"/login.html");

```
前端: 通过ajax的complete方法
```bash
$.ajaxSetup({
  complete: function(XHR){
    if("REDIRECT" === XHR.getResponseHeader("REDIRECT")){
       var url = XHR.getResponseHeader("CONTENTPATH");
       windows.location.href = url; 
    }
  }
})
```

### JSONP
原因: jsonp的本质是script标签, 所以通过是获取不到请求头的。getResponseHeader的值一直为空。

### CORS
原因: 通过CORS方式解决的ajax跨域,是获取不到请求头的。getResponseHeader的值一直为空。
解决: 通过Access-Control-Expose-Headers来设置响应头的白名单。
```
httpResponse.addHeader(“Access-Control-Expose-Headers”, “REDIRECT,CONTEXTPATH”);将想要传递的字段设置一下。才能获取到值。
```



### 其他
https://blog.csdn.net/mozha_666/article/details/86519642


