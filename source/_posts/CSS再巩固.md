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
     - 如果div中只有内联元素，那么div的高度就是又内联元素的行高`line-height`决定的
   - 文档流就是**文档内元素的流动方向**（什么是文档流？）
     - 内联元素从左往右流动
     - 块级元素从上往下流动
   - 对于内联元素（inline），有一个叫做`word-break`的属性，可以用来设置单词是如何换行的。

4. 单行文字溢出：

   - 单行文本设置文本不自动响应式换行：

     ```css
     white-space: nowrap;
     ```

   - 超出部分被省略号替代

     ```css
     overflow: hidden;
     text-overflow:ellipsis;
     ```

5. 文字垂直居中

   - 不要去设置div的height，用line-height和padding去自动撑开div

     ```css
     line-height: 28px;
     padding: 10px 0;
     ```

6. **margin合并**

   - 一个父div里有一个子div，那么父子div的margin-top和margin-bottom会合并

     ```css
     .son{
         border: 15px solid red;
         padding: 10px;
         margin: 10px;
     }
     .dad{
         outline: 3px solid green
     }
     ```

   - 有一下几种方法可以解决margin合并（核心思想是只要有“东西”可以挡住子元素的margin那么就可以防止margin合并）

     - 给父元素加border（可以挡住）
     - 给父元素加margin（可以挡住）
     - 给父元素加padding（可以挡住）
     - 给父元素加overflow: hidden（不推荐，因为会产生新的bug，如使用float给另一子元素，可能就会被hidden）

7. 「姓名」与「联系方式」两端对齐

   ```css
   span{
     border: 1px solid red;
     width: 5em;
     display: inline-block;
     text-align: justify;
     line-height: 20px;
     height: 20px;
     padding: 10px 0;
     overflow: hidden;
   }
   span::after{
     content: '';
     width: 100%;
     display: inline-block;
     border: 1px solid black;
   }
   ```

8. **BFC** （block formatting context）

   1. 用BFC可以包住浮动元素
   2. 让两个相邻的元素界限分明
      - 举例：如果左边有一个float元素，右边有个block，那么不触发BFC的情况就是两个元素会重叠。如果我们想让两个元素界限分明就给block元素触发BFC
   3. 触发BFC的几种方法：
      - CSS3新属性，`display: flow-root`的功能只有一个就是触发BFC
      - `overflow: hidden;`
      - `display: inline-block;`
      - `display: table-cell;`
      - 变成绝对定位`position: absolute;`

9. **REM**（网页默认的font-size是16px）

   1. 什么是rem？

      - 这个单位代表根元素（HTML）的`font-size`大小

   2. 在哪里设置rem？

      ```css
      html{
          font-size: 100px;
      }
      ```

   3. 一般会用JS将设备宽度赋值给html的`font-size`

      ```js
      var pageWidth = window.innerWidth;
      document.write(`<style>html{font-size: ${pageWidth}px; }</style>`)
      ```
