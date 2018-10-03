---
title: JS回顾系列（二）
date: 2018-09-30 16:39:44
tags: JavaScript
---

#### 常用api：

1. `node.nodeType`，`1`表示节点，`3`表示文本。使用情景：因为nextSibling有bug（有些浏览器内核认为两个tag之间存在回车，所以nextSibling可能会取到回车） 

   1. ```js
      let bro  = target.nextSibling;
      while(bro.nodeType === 3){
          bro = bro.nextSibling;
      }
      ```

2. `node.tagName`返回的值是大写字母，如`<ul></ul>`的tagName为`'UL'`

3. `document.querySelectorAll('#div ul li');`

4. `node.parentNode.children`

#### JS动画与缓动

```js
div.style.position = "relative";
div.style.left = 0;
var n = 0;
var id = setInterval(()=>{
    n = n + 1;
    div.style.left = n + 'px';
    if (n > 200) {
        window.clearInterval(id);
    }
}, 40)
```

- 实用插件：[tween.js](https://cdnjs.cloudflare.com/ajax/libs/tween.js/17.2.0/Tween.min.js)

### Array

1. `let a = ['a','b']`等价于`let a = new Array('a','b')`

2. #### forEach()

   `forEach(function(x, y))`，`forEach()`接受的是**函数**，函数必须接受两个参数，前者是`value`，后者是`index`

3. #### sort()

   `array.sort()`默认为正序排序，`sort`可以接受一个函数作为参数来改变排序顺序。如：

   - `array.sort((x, y) => x-y)`正序

   - `array.sort((x, y) => y-x)`倒序

   - ```js
     // 同理可以根据hash的value来排序 
     let a = ['apple', 'banana', 'palm'];
     let hash = {'apple': 10, 'banana': 5, 'palm': 20};
     array.sort( (x, y) => hash[x] - hash[y] ); // ['banana', 'apple', 'palm']
     ```

4. #### join()

   - 和Python的join用法一样，用于数据转换成字符串

   - ```js
     let a = [1,2,3];
     let str = a.join('+') // "1+2+3"
     ```

5. #### concat()

   - 用于连接合并两个数组。在JavaScript中，数组a + 数组b的结果是两个数组.toString()后进行字符串的合并，并不可以用于合并两个数组。所以需要`concat()`方法。

   - ```js
     let a = [1,2,3];
     let b = [4,5,6];
     a.concat(b) // [1,2,3,4,5,6]
     ```

   - **也用于复制一个数组（深度拷贝）**

   - ```js
     let a = [1,2,3];
     let b = a.concat([]);
     b === a // false
     ```

6. #### map()

   - `map`和`forEach`几乎是一模一样的，唯一不同的地方在于`forEach`运行完之后不会返回任何值，而`map`会将运行结果重新生成一个新数组进行返回。

   - ```js
     let a = [1,2,3];
     a.forEach(function(x, y){
         return x * 2;
     })
     // undefined
     
     a.map(function(x, y){
         return x * 2;
     })
     // [2,4,6]
     // 用ES6可以更美观地写成
     a.map(value => value * 2)
     // [2,4,6]
     ```

7. #### filter()

   ```js
   // 得到所有偶数的平方
   let a = [1,2,3,4,5,6,7,8,9];
   a.filter((x) => {
       return x % 2 === 0;
   }).map((x) => {
       return x * x;
   })
   ```

8. #### reduce()

   ```js
   // 计算所有奇数的和
   let a = [1,2,3,4,5,6,7,8,9];
   a.reduce((sum, n) => {
       if(n % 2 === 1) {
           sum += n;
       }
       return sum;
   }, 0)
   ```
