---
title: 浏览器也会偷懒-解决无缝轮播的bug
date: 2018-10-20 11:51:50
tags:
---

实现无缝轮播的时候可能会遇到一个小bug：

当切换到别的页面几秒钟后再切换回原来的轮播页面，会发现轮播图从切出那刻开始就停止，切回来的时候会在短时间内快速完成之前几秒应该做完的轮播，也就是说浏览器在你不“看”它的时候偷懒了，而等你“看”它的时候心虚一样快速的完成之前偷懒的工作。这样用户的体验就是很好了。

> 解决的办法是当页面切出时，通过监听`visibilitychange`事件来判断页面是否切出并控制轮播启停。

```javascript
let n = 1;
let timer = setInterval(function () {
    $(`.img-wrap img:nth-child(${getIndex(n)})`).removeClass("current").addClass("leave").one('transitionend', (e) => {
        $(e.currentTarget).removeClass("leave").addClass("enter");
    });
    $(`.img-wrap img:nth-child(${getIndex(n + 1)})`).removeClass(" enter").addClass("current");
    n++;
}, 3000);

document.addEventListener('visibilitychange', function (e) {
    if (document.hidden) {
        window.clearInterval(timer);
    } else {
        timer = setInterval(function () {
            $(`.img-wrap img:nth-child(${getIndex(n)})`).removeClass("current").addClass("leave").one('transitionend', (e) => {
                $(e.currentTarget).removeClass("leave").addClass("enter");
            });
            $(`.img-wrap img:nth-child(${getIndex(n + 1)})`).removeClass(" enter").addClass("current");
            n++;
        }, 3000);
    }
})
```

另外目前轮播比较好的插件是[Swiper](https://www.swiper.com.cn/demo/index.html)