---
title: 在前端引入MVC思想以及会遇到的问题
date: 2018-10-23 23:43:52
tags: MVC
---

MVC是Modal, View and Controller的缩写，在前端引入MVC思想可以更有助于我们对于前端框架的学习。

不似springMVC，我们现在可以简单的把前端不同功能的`function`分为不同的`Modal`。而每一部分`Modal`对应的视图部分我们可以称之为`View`，在每个`Modal`里，控制对应`View`的部分称之为`Controller`。

在引入`MVC`思想之后，发现我们并不想要全局变量而想使用局部变量，可在ES 5中，只有函数才具有局部变量，于是我们声明一个function并且立即执行，如

```js
function(){}.call();
```

但是这种写法在Chrome中会报错说语法错误，所以我们需要使用下述写法：

```js
!function(){}.call(); // 我们不在乎这个匿名函数的返回值，所以加个!取反没关系
```

下面举个例子:

```js
!function(){
    var persion = {
        name: 'frank',
        age: 18
    }
}.call();
```

在上面的例子中，立即执行函数使得`person`无法被外部访问，但若我们一定要操作`person`应该怎么办呢？我们可以使用`闭包`：

```js
!function(){
    var persion = {
        name: 'frank',
        age: 18
    }
    window.ageGrowUp = function(){
        person.age += 1;
        return person.age;
    }
}.call();
```

所以`window.ageGrowUp`保存了匿名函数的地址，任何地方都可以使用`window.ageGrowUp`来操作`person.age`，但是不能直接访问`person`