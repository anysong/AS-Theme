### URL传中文参数导致乱码的解决方案

#### 背景(为什么要编码)
> 当使用地址栏提交查询参数时，如果不编码，非英文字符会按照操作系统的字符集进行编码提交到服务器    
> 服务器会按照配置的字符集进行解码，所以如果两者不一致就会导致乱码。

#### 一次encodeURIComponent编码的情况：
```
前端
var encodeUrl = encodeURIComponent("http://www.test.com/s?state=1&paramName=张三");
后端
String paramValue = request.getParameter(paramName);  

# 用getParameter接收后，Tomact会自动解码，
# 如果Tomact接收请求的编码格式是UTF-8的话，解码后没有问题；
# 如果不是UTF-8的话就会出现乱码
```
#### 一次encodeURIComponent编码的(前端)扩展
```
前端
window.location.href = "//www.test.com/Search?keyword=" + encodeURIComponent(KEYWORD) + "&enc=utf-8";
# 标注编码方式 enc=utf-8
```
#### 为什么encodeURIComponent / encodeURI编码时要编码两次
> encodeURI使用的是 UTF-8 编码规则来编的，当服务器接收url的参数后会自动解码一次  
> 但自动解码的字符集不一定是UTF-8，字符集不一致时解码会出现乱码。

#### 两次encodeURIComponent编码的情况：
```
前端
var Url = encodeURIComponent("http://www.test.com/s?state=1&paramName=张三");
var Url2 = encodeURIComponent(encodeUrl);
后端
String name1 = request.getParameter(paramName);
String name2 = java.net.URLDecoder.decode(name1,"UTF-8");

# Url是将中文编码成ASCII码后的URL；
# Url2是将ASCII码编码后的URL，由于用GBK、UTF-8、ISO-8859-1对ASCII码编码的结果是相同的，
# 所以request.getParameter("name")解码的时候，不管是按 GBK 还是 UTF-8 还是 ISO-8859-1 都好，都能够正确的得到URL。
```

#### 补充如何设置Tomcat接收请求的编码格式：
> 可以利用request.setCharacterEncoding("UTF-8");来设置Tomcat接收请求的编码格式，  
> 但是只对POST方式提交的数据有效，对GET方式提交的数据无效!  
> 要设置GET的编码，可以修改server.xml文件中，相应的端口的Connector的属性：URIEncoding="UTF-8"，  
> 这样，GET方式提交的数据才会被正确解码。

#### ASCII码
#### 总结
###### 问题
+ 当使用地址栏提交查询参数时，如果不编码，非英文字符会按照操作系统的字符集进行编码提交到服务器。
+ IE、 Firefox、Chrome浏览器对URL的编码方式各不相同。
+ 而服务器只能以一种编码方式来对接收到的URL进行解码。(可通过传参数,指定"&enc=utf-8")
+ 服务器会按照配置的字符集进行解码，所以如果两者不一致就会导致乱码。
###### 解决
+ 前端执行两次encodeURIComponent编码
+ 第一次执行返回ASCII码
+ 第二次执行返回将ASCII码编码后的URL
+ 由于用GBK、UTF-8、ISO-8859-1对ASCII码编码的结果是相同的
+ 所以后端只需要解码一次,都能够正确的得到URL
+ 后端不管是按GBK还是UTF-8还是ISO-8859-1解码的结果都是相同的

#### 思考
有种说法是,如果能保证编码方式是UTF-8,且解码可配UTF-8的话,只需要转码一次
> 一般情况下, 发送 encodeURIComponent(parmeName)+"="+encodeURIComponent(parmeValue);  
> 接收时, 直接 String paramValue = request.getParameter(paramName); // 容器自动解码.  
> 我们知道 encodeURIComponent 使用的是 UTF-8 编码规则来编的.  
> 如果 request.getParameter(paramName) 时,容器也按 UTF-8 解的话,是正确的.   
> 根本无须在客户端进行二次的 encodeURIComponent(...)  
> 如果 request.getParameter(paramName),容器没有按 UTF-8 解的话, 结果只有一个,就是乱码!  
> 容器按什么编码来解码,决定于 request.setCharacterEncoding(***) 或者 服务器程序配置.  
> 如果你在 jsp 程序中,能够 request.setCharacterEncoding("UTF-8"),  
> 并且 修改服务器配置,让容器在解 GET 提交的参数时,使用 UTF-8.  
> 客户端提交前不用二次编码, 接收时,也只要直接 request.getParameter(paramName) 即可  


#### 参考
https://www.cnblogs.com/menggirl23/p/10438371.html
https://www.jianshu.com/p/831618a8e116

