---
title: JS简单类型和对象的区别
date: 2018-09-29 22:44:58
tags: JavaScript
---

简单类型与对象的主要区别就是简单类型是存储在栈内存当中的，而对象是存储在堆内存当中的。

1. `var a = 1`和`var a = new Number(1)`的区别：

   前者是简单类型，后者是对象。后者具有一些内在API如`toExponential()`, `valueOf()`, `toString()`等

   但其实前者也可以直接使用这些API，是什么原因呢？

   > JS之父在开发语言中，会在简单类型欲调用API时，先创建一个临时对象，比如对于number类型就会创建一个`var tmp = new Number(a)`，当调用API时，实际是临时对象在调用。

2. String的常用API介绍

   1. `trim()`:  去掉头尾空格
   2. slice(0, 2): 切片
   3. includes('a'): 是否有某个字符
   4. chartAt(2): index为2的地方是哪个字符
   5. IndexOf('a'): 查看某个字符的index