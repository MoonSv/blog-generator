---
title: 自制简易jQuery
date: 2018-10-06 00:01:11
tags: jQuery, JavaScript
---

### 需求：

```js
window.jQuery = ???
window.$ = jQuery

var $div = $('div')
$div.addClass('red') // 可将所有 div 的 class 添加一个 red
$div.setText('hi') // 可将所有 div 的 textContent 变为 hi
```

### 思路

jQuery 类似一个封装好的函数，提供给我们各种方法，同样的需求下，使用 jQuery 让开发者少敲很多代码并且解决不同浏览器兼容性的问题。

1. 封装函数

   ```js
   function getSiblings(node){
       // write some code...
   }
   ```

2. 命名空间

   命名空间可以防止污染全局变量。

   ```js
   var jQuery = {}
   jQuery.getSiblings = function(node){ 
       // write some code...
   }
   jQuery.setText = function(node){
       // write some code...
   }
   
   // 调用函数时
   jQuery.getSiblings(node)
   jQuery.setText(node)
   ```

3. 把node提前

   ```js
   // 调用函数时
   node.getSiblings()
   $node.getSiblings()
   ```

   事实上， jQuery 的属性和方法保存于 jQuery.prototype。不过这里不采用这种方法。

   - 方法一：扩展 Node 接口。直接在 Node.prototype 上加函数。可能的风险是覆盖原生的属性和方法。

     ```js
     Node.prototype.getSiblings = function(){
         // write some code...
     }
     ```

   - 方法二：添加新的接口。这叫做「无侵入」。

     ```js
     window.jQuery = function(nodeOrString){
                 let nodes = {};
                 if (typeof nodeOrString === 'string'){
                     var tmp = document.querySelectorAll(nodeOrString);
                     for (var i = 0; i < tmp.length; i++) {
                         nodes[i] = tmp[i];
                     }
                     nodes.length = tmp.length;
                 } else if (nodeOrString instanceof node){
                     nodes = {
                         0: nodeOrString,
                         length: 1
                     }
                 }
                 nodes.addClass = function(classes){
                     for(var i = 0; i < nodes.length; i++) {
                         nodes[i].classList.add(classes);
                     }
                 }
                 nodes.setText = function(text){
                     for(var i = 0; i < nodes.length; i++) {
                         nodes[i].textContent = text;
                     }
                 }
                 return nodes;
             }
     window.$ = jQuery
     
     var $div = $('div')
     $div.addClass('red') // 可将所有 div 的 class 添加一个 red
     $div.setText('hi') // 可将所有 div 的 textContent 变为 hi
     ```



#### jQuery细碎知识点

1. .eq(n)会找到第n个对象**并将对象封装成一个jQuery对象**