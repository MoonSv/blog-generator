---
title: CSS再巩固
date: 2018-09-23 13:41:57
tags:css
---

1. 手写导航栏知识点
   - 浮动布局

     - `float: left`

   - 清除浮动

     - 给fload的父级元素加clearfix类

     - ```css
       .clearfix::after{
       	content: '';
         	display: block;
         	clear: both;
       }
       ```

2. 页面默认字体大小为16px，可以通过chrome开发者工具Elements右侧Computed一栏输入`font-size`查到

3. 高度与文档流

   - **div 高度由其内部文档流元素的高度总和决定**
   - 文档流就是**文档内元素的流动方向**（什么是文档流？）
     - 内联元素从左往右流动
     - 块级元素从上往下流动
   - 对于内联元素（inline），有一个叫做`word-break`的属性，可以用来设置单词是如何换行的。