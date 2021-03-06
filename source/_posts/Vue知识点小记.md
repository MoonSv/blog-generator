---
title: Vue知识点小记
date: 2019-01-09 11:18:22
tags:
---

1. Vue中只要是大写字母都会转换成    `-`小写

   如fontSize ---> font-size

   1. 使用`:style`时。Vue.js会自动给特殊的css属性名称增加前缀，如`transform`

2. `v-if`和`v-show`的区别：

   - `v-if`实时渲染，页面显示就渲染，不显示就直接从DOM树中移除
   - `v-show`永远存在于DOM树中，只是通过切换`display`来展现与否

3. `v-if`的弊端

   Vue在渲染元素时，出于效率考虑，会尽可能地复用已有的元素而非重新渲染，因此会出现乌龙

   只会渲染变化的元素，也就是说，input元素被复用了

   解决方法：加`key`唯一标识

4. 组件

   1. 必须使用小写字母加'-'的方式进行命名
   2. `template`必须被标签包裹

5. 子组件向父组件传数据三步走：

   1. 自定义事件
   2. 在子组件中用`$emit`出发时间，第一个参数是事件名，后边的参数是要传递的数据
   3. 在自定义事件中用一个参数来接受

6. 父组件需要拿子组件的内容时，如果用`$child`则分不清拿到的是哪个子组件。

   可以通过给子组件添加`ref=''`这个属性来为子组件添加索引。如

   ```html
   <child-component ref='a'></child-component>
   ```

   这是在父组件的方法中可以通过

   ```js
   this.msgFromChild = this.$refs.c.msg;
   ```

   来拿到目标子组件数据

7. 自定义指令

8. Vue实现点击动画，并可无限点击

   原理是通过v-bind绑定类名，通过点击事件给元素添加`active`类名来出发动画。

   动画原理：动画效果为点击刷新icon进行rotate，使用`keyframes`来呈现旋转效果，简单css代码如下

   ```css
   .refresh-button {
     color: rgb(141, 150, 151);
     cursor: pointer;
     font-size: 26px;
   }
   .refresh-button.active{
     animation: rotate 0.6s;
   }
   @keyframes rotate {
     0%{
       transform: rotate(0deg);
       color: rgb(141, 150, 151);
     }
     50%{
       color: rgb(216, 101, 101);
     }
     100%{
       transform: rotate(-360deg);
       color: rgb(141, 150, 151); 
     }
   }
   ```

   使用Vue中的缩写`@`代替`v-on:`， `:`代替`v-bind:`

   ```html
   <i class="el-icon-refresh refresh-button" @click="refreshData" :class="{active: isActive}"></i>
   ```

   在Vue中写的方法为

   ```js
   refreshData() {
       this.isActive = true;
       // set timeout to reset rotate animation
       setTimeout(()=>{
           this.isActive = false
       }, 600)
   }
   ```

   注意这里要使用`setTimeOut()`来重置属性。