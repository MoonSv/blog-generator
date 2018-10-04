---
title: 'DOM(API, event)，虚拟DOM深入理解'
date: 2018-10-04 14:06:26
tags: DOM, 虚拟DOM
---

### 1. DOM简介

Document Object Model: 把文档和对象对应起来的模型叫DOM

- `meta`, `title`, `script`, 等等都是**Element**对象， `html`属于**Document**对象
- `h1`, `h2`, `p`等中的文本属于**Text**对象。
- 注释属于**Comment**对象
- 这3种对象有一个共同的祖先：**Node**
- DOM的最小组成单位叫做**Node**
- DOM树的根节点是`HTML`

### 2. 碎知识整理

1. Node的接口（属性和方法）

- innerText和textContent区别：前者是由IE浏览器引入的，后者是之后由Firefox和Opera引入的. **`textContent`**会获取所有元素的内容，包括<font color=darkgreen> script标签和style标签里的文字内容 </font>
- `removeChild()`只是将元素从页面中移除，但内存中还存在
- nextSibling可能会获取到文本，因为在html中，标签之间的<font  color=darkgreen>回车</font>属于文本
- nodeType需要背，<font color=darkgreen>1表示节点，3表示文本</font>
- cloneNode()可以传参数`true`来表示是否为深度克隆，深度克隆会将所有的子元素都克隆下来
- `parent.childNodes` 是**动态集合**。所谓动态集合就是一个活的集合，DOM树删除或新增一个相关节点，都会立刻反映在NodeList接口之中。
- `document.querySelectorAll`方法返回的是一个**静态集合**。DOM内部的变化，并不会实时反映在该方法的返回结果之中。

