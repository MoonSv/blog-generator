---
title: JS回顾系列（一）
date: 2018-09-29 14:49:57
tags:
---

### JavaScript数据类型

1. ##### JS中7中数据类型

   - `Number`, `null`, `undefined`,  `String`, `Symbol`, `Boolean`,`Object`
   - 其中，除`Object`外的前6种数据类型被称为**基本类型**或**简单类型**

2. ##### `Number`

   - `Number`中需要记忆的点是
     - 二进制都是以0b开头，如0b11为3（十进制），
     - 八进制以0开头，如`011`为9（十进制）。这是一个需要注意的点，例如电话号码`0105176531`就不能存成Number形式，否则会被认为是八进制，应该存成String类型。
     - 十六进制以0x开头，如`0x11`为17（十进制）。

3. ##### `null`和`undefined`

   - 如果变量没有值，那么就是`undefined`。
   - 惯例：
     - 如果有一个对象，但现在不想给值，那么就给一个`null`。
     - 如果有一个非对象(number, string等)，但现在不想给值，那么就给一个`undefined`。

4. ##### `Object`

   - 对象中的key的格式为字符串，但在定义时可以加引号也可以不加，但如果不加引号则必须满足标识符规范。
   - 取key时可以写成`person['name']`，当引号内的值满足标识符规范的情况下，可以写成`person.name`
   - **`in`**， 可以用`in`来判断该对象是否有某属性，如`'name' in person`返回true存在，false不存在。
   - **删掉**`object`中某属性：`delete person['name']`
   - **`for...in`**，遍历`object`
   - `typeof`查看变量属于什么类型

### JavaScript里的数据类型转换

1. ##### 其他类型转为string

   - 可以采用`xx.tostring()`方法，但对null支持不加
   - 全局函数`String(xx)`
   - **更流行**的方法是`xx + ''`

2. ##### 转为boolean

   - 全局方法`Boolean(xx)`。这里**需要记住的一点**是：
     - `Boolean('')`的值为`false`而`Boolean({})`的值为`true`
   - **要记住5个falsy值**（falsy是在Boolean上下文中认定可转换为false的值）
     - number里的`0`和`NaN`
     - string里的`''`
     - `null`
     - `undefined`
   - 所有的对象都是`true`

3. ##### 转为number

   - 全局方法`Number('1')`
   - `parseInt('1', 10)`，`parseInt('123silence', 10)`这里会解析到123
   - `parseFloat('1.23')`
   - `'1' - 0 `这种方法被程序员广泛使用
   - `+ '1'`

### JavaScript 内存

- 在JavaScript中，有内存被分为stack（栈内存）和heap（堆内存）。

- 所有简单数据类型（6个）都会被存在栈内存。

- 而复杂类型会在栈内存中存一个地址，地址指向堆内存的某个区域，这个区域存放着实际的数据。

**3个内存题目：**

1. 

   1. ```js
      var a = {name : 'Jack'};
      var b = a;
      b = {name: 'Lorry'};
      a['name'] = ?    // Jack
      ```

2. 

   1. ```js
      var a = {name: 'Jack'}；
      var b = a;
      b.name = 'Lorry';
      a['name'] = ?    // Lorry
      ```

3. 

   1. ```js
      var a = {name: 'Jack'}；
      var b = a;
      b = null;
      a = ?    // {name: 'Jack'};
      ```

4. 这里的考点是在第3行的`a.x`其实还是原来的a，后面a又有了新地址，所以x是给了原来的老地址，而b一直指向的是老地址

   1. ```js
      var a = {n: 1}；
      var b = a;
      a.x = a = {n: 2}
      a.x = ?    // undefined 
      b.x = ?    // [object Object]
      ```

### 垃圾回收

###### 什么是垃圾？

- 如果一个对象没有被引用，那么它就是垃圾

###### 题目

```js
var fn = function(){};
document.body.onclick = fn;
fn = null;
// function(){}是不是垃圾？
// 答案是否定的，通过想象内存图可得知function()依然被document.body.onclick所引用着
```

### 数组

1. #### 数组的本质

   本质上，数组属于一种特殊的对象。`typeof`运算符会返回数组的类型是`object`。

2. length属性

   - 数组的`length`属性，返回数组的成员数量。

   - `length`属性是可写的。如果人为设置一个小于当前成员个数的值，该数组的成员会自动减少到`length`设置的值。

   - ```js
     var arr = ['a', 'b', 'c'];
     arr.length //3
     
     arr.length = 2;
     arr // ['a', 'b']
     ```

     上面代码表示，当数组的`length`属性设为2（即最大的整数键只能是1）那么整数键2（值为`c`）就已经不在数组中了，被自动删除了。

     清空数组的一个有效方法，就是将`length`属性设为0。