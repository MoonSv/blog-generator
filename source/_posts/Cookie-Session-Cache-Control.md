---
title: 'Cookie, Session, Cache-Control'
date: 2018-10-29 14:09:52
tags: Cookie, Session, Cache-Control
---

1. #### Cookie

   1. 服务器通过`Set-Cookie`头给客户端一串字符串
   2. 客户端每次访问**相同域名**的网站是，必须带上这段字符串
   3. 客户端要在一段时间内保存这个`Cookie`
   4. `Cookie`默认在用户关闭页面后就失效，后台代码可以任意设置`Cookie`的过期时间

2. #### Seesion

   1. 将`SeesionID`（随机数）通过`Cookie发给客户端
   2. 客户端访问服务器时，服务器读取`SessionID`
   3. 服务器有一块**内存**（哈希表）保存了所有`session`
   4. 通过`SessionID`我们可以得倒对应用户的隐私信息如`id`, `email`等
   5. 这块**内存**（哈希表）就是服务器上的所有`session`

3. #### LocalStorage

   1. `LocalStorage`跟`HTTP`无关
   2. `HTTP`不会带上`LocalStorage`的值
   3. 只有相同域名的页面才能互相读取`LocalStorage`
   4. 每个域名`LocalStorage`最大存储量为5Mb（每个浏览器不一样）
   5. 常用场景：记录有没有提示过用户（等不敏感的信息）
   6. `LocalStorage`永久有效，除非用户清理缓存

4. #### SessionStorage

   1. 前四点同上
   2. `SessionStorage`在用户关闭页面后就失效

5. #### HTTP缓存

   1. 设置`Cache-Control`**响应头**来进行web性能优化

      ```js
      response.setHeader('Cache-Control', 'max-age=31650000')
      ```

      1. 可以让你的浏览器在一定时间内不访问服务器，直接访问本地的硬盘，这样速度会极快（因为请求都不会被发出去）。
      2. 知乎设置Cache-Control的`max-age`为365天
      3. 如果需要更新，可以直接在入口处`url`稍微变一下，跟以前的所有`url`都不一样，这样浏览器就会发送请求，去更新网页。

   2. 设置`Expires`**响应头**来进行web性能优化

      ```js
      response.setHeader('Expires', 'Sun, 04 Feb 2018 18:11:05 GM')
      ```

      这是一种老的做法，和`Cache-Control`相比，`Expires`设置的是过期的时间点，`Cache-Control`设置的是时间段。如果用户的系统时间错乱那么`Expires`就会有bug。