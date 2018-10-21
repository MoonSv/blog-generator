---
title: 同源策略与CORS跨域
date: 2018-10-22 01:13:26
tags:
---

Question: 为什么form等请求可以跨域，而AJAX请求无法跨域？

> 因为原页面用form提交到另一个域名之后，原页面的脚本无法获取新页面中的内容。
>
> 所以浏览器认为这是安全的。
>
> 而AJAX是可以**读取相应内容的**， 因此浏览器不能允许你这样做。
>
> 如果你细心的话会发现，其实请求已经发送出去了，你只是拿不到响应而已。
>
> 所以浏览器这个策略的本质是，一个域名的JS，在未经允许的情况下，不得读取另一个域名的内容。但浏览器并不阻止逆向另一个域名发送请求。

#### 1. 同源策略

<https://earthsplitter.github.io/2017/03/21/%E5%90%8C%E6%BA%90%E6%94%BF%E7%AD%96%E4%B8%8E%E8%B7%A8%E5%9F%9F%E8%AF%A6%E8%A7%A3/>

- 协议相同(FTP, HTTP)

- 域名相同

- 端口相同

  目的: 为了保护用户隐私，防止身份伪造等 

#### 2. JSONP 

- 优点：兼容性好 

- 缺点：仅支持GET方法具有局限性 
- 其设计思路是浏览器对<script>标签不做限制，因此可以利用这一点进行跨域请求 
- 很简单，就是利用<script>标签没有跨域限制的“漏洞”（历史遗迹啊）来达到与第三方通讯的目的。当需要通讯时，本站脚本创建一个<script>元素，地址指向第三方的API网址，形如：<script src="<http://www.example.net/api?param1=1¶m2=2>"></script> 并提供一个回调函数来接收数据（函数名可约定，或通过地址参数传递）。第三方产生的响应为json数据的包装（故称之为jsonp，即json padding），形如：callback({"name":"hax","gender":"Male"})。这样浏览器会调用callback函数，并传递解析后json对象作为参数。本站脚本可在callback函数里处理所传入的数据。补充：“历史遗迹”的意思就是，如果在今天重新设计的话，也许就不会允许这样简单的跨域了嘿，比如可能像XHR一样按照CORS规范要求服务器发送特定的http头。 

#### 3. CORS<https://www.jianshu.com/p/94946ca90194> 

- 优点：功能更强大支持HTTP各种method 

- 缺点：兼容性不如JSONP，要求IE>10 
- 服务端：若确定接受请求，则在返回结果中加入响应头：Access-Control-Allow-Origin，值为请求方的域名
- CORS的核心就一句话，在服务器端设置响应头

```javascript
response.setHeader('Access-Control-Allow-Origin', 'frontendSite');
```



