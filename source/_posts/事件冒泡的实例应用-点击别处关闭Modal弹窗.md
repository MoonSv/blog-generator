---
title: 事件冒泡的实例应用---点击别处关闭Modal弹窗
date: 2018-10-19 11:17:45
tags: 事件, 冒泡
---

学习了事件模型之后，发现概念可以背的滚瓜烂熟，但是对于事件冒泡和事件捕获究竟在什么场景使用还是比较模糊，所以这里介绍一个简单的**例子**可以帮助更好的理解**事件冒泡**。

```html
<style>
    .wrapper{
        position: relative;
        display: inline-block;
        transition: all 0.3s;
    }
    .modal{
        border: 1px solid grey;
        border-radius: 5px;
        position: absolute;
        left: 100%;
        top: 0;
        white-space: nowrap;
        padding: 10px;
        margin-left: 10px;
        display: none;

    }
    .modal::before{
        content: '';
        border: 10px solid transparent;
        border-right: 10px solid grey;
        position: absolute;
        right: 100%;
        top: 3px;
    }
    .modal::after{
        content: '';
        border: 10px solid transparent;
        border-right: 10px solid #fff;
        position: absolute;
        right: 100%;
        top: 3px;
        margin-right: -1px;
    }
</style>
<div class="wrapper">
    <button class="click">
        click me
    </button>
    <div class="modal">
        This is the modal content
    </div>
</div>
<script>
    $(".wrapper").click(function(e){
        e.stopPropagation();
        $(".modal").show();

    })
    $("html").click(function(){
        $(".modal").hide();
    })
</script>
```

在这里通过对wapper添加阻止事件传播`e.stopPropagation()`来阻止冒泡。

------

以上是通过阻止事件传播的方法，下面介绍一种优化的省内存方法

```javascript
$(".wrapper").on('click', function(){
    $(".modal").show();
    $(document).one('click', function(){
        $(".modal").hide();
    })
})
```

这样写的好处是在`document`上绑定的click事件只会在每次点击`wrapper`的时候绑定一次。