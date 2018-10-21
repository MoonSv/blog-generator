---
title: JSONP
date: 2018-10-21 23:01:51
tags: JSONP
---

JSONP不是什么高大上的东西，简单地来说：

请求方：frontend.com (浏览器)

响应房：backend.com (服务器)

1. 请求方创建动态`script`，其中标签的`src`指向响应方，假设请求方的回调函数名称是`renderPayment`，我们就需要同时传一个查询参数`callbackName=renderPayment`给响应方

   ```html
   <button id="click">click me</button>
   <script>
       click.addEventListener('click', function(){
           let script = document.createElement("script");
           let functionName = 'f' + parseInt(Math.random() * 100000, 10);
           window[functionName] = function(result){
               console.log(`the result from back end is ${result}!`);
           }
           script.src = `127.0.0.1:8001/pay?callbackName=${functionName}`
           document.body.appendChild(script);
           
           // delete script tag when finish the request
           script.onload = function(e){
               e.currentTarget.remove();
           }
       })
   </script>
   ```

   当然我们可以使用jQuery用更简洁的代码实现：

   ```html
   <script>
       $.ajax({
           url: '127.0.0.1:8001/pay',
           dataType: 'jsonp',
           success: function(response){
               console.log(`the result from back end is ${response}!`);
           }
       })
   </script>>
   ```

2. 响应方根据查询参数`callbackName`，构造类似

   - `renderPayment.call(undefined, '请求方要的数据')`
   - `renderPayment('请求方要的数据')`

   这样的响应

   ```javascript
   if (path === '/pay'){
       let amount = fs.readFileSync('./db', 'utf8')
       amount -= 1
       fs.writeFileSync('./db', amount)
       let callbackName = query.callback
       response.setHeader('Content-Type', 'application/javascript')
       response.write(`
           ${callbackName}.call(undefined, 'success')
       `)
       response.end()
   }
   ```

3. 浏览器接收到响应后，就会执行`renderPayment.call(undefined, '请求方要的数据')`

4. 那么请求方就获得了想要的数据并且完成处理

**这就是JSONP**



下面是一些约定成俗的东西：

1. GET请求中的查询参数通常为`callback`
2. 回调函数名通常为`非数字+随机数`，如`j48174940`



最后记录一道面试题：为什么JSONP不支持POST请求？

Answer：

1. 因为`JSONP`是通过动态创建`scirpt标签`实现的
2. 动态创建`script`的时候只能用`GET`，无法使用`POST`