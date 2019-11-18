## 解决ajax不能重定向问题
首先需要确认XHR,JSONP,

#### XHR
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

#### JSONP
jsonp的
