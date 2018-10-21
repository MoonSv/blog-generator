---
title: onclick事件应该怎么写
date: 2018-10-18 15:17:39
tags:
---

#### DOM level 0

在html中写onclick事件有如下几个选项

```html
function print(){
	console.log('hello')
}
<button id="x" onclick="print"></button>
<button id="y" onclick="print()"></button>
<button id="z" onclick="print.call()"></button>
```

正确的是第二个和第三个，因为因为一旦用户点击，浏览器就会默认调用`eval()`，所以`print()`和`print.call()`都会调用`print`这个函数，而第一个无法调用。



在JavaScript中的onclick写法有如下几个选项

```javascript
x.onclick = print;
y.onclick = print();
z.onclick = print.call();
```

那么正确的是id为x的button绑定的写法，一旦用户点击，浏览器就执行`x.onclick.call(x, {});`

#### DOM level 2

在DOM level 2中。事件绑定（监听）就变成了这种写法`xxx.addEventListener('click', function(){})`，与DOM level 1的区别是：**在level0中，事件（如click）只能被绑定一次，如果重复绑定后面的会覆盖之前已经绑定的函数，但在level2中，使用`addEventListener()`函数可以给事件绑定多个函数，这些函数以队列的形式（先进先出）被绑定，当触发事件时会执行先被绑定的函数**

```javascript
xxx.addEventListener("click", function(){
    console.log(1);
})
xxx.addEventListener("click", function(){
    console.log(2);
})
xxx.addEventListener("click", function(){
    console.log(2);
})
```

当用户点击`xxx`时，会依次打印出`1`, `2`, `3`

- `one`和`on`的区别， `one`绑定的事件当触发式只会调用一次，而`on`绑定事件的函数会永久绑定
- DOM level 2中添加了**事件捕获**和**事件冒泡**，前者从外至内，后者从内至外。顺序是先捕获，再冒泡。当同一个元素绑定了捕获和冒泡时，先执行先被绑定的