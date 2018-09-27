---
title: React Router4.0
date: 2018-08-22 11:50:02
tags:
---

#### 路由模块安装

- npm install react-router-dom —save

遇到不想加载多个路由的时候就用Switch方式（只会加载第一个匹配的路由）

router的根元素是HashRouter

App组件里面写{this.props.children}可以用来处理和主页平行的那些页面(Login等)

函数传参，参数用[]包起来才表示为变量



Switch值渲染命中的第一个route



跳转页面 window.location.href = ``

 vport除了主页之外都是common.js通用页面



通过router取动态变量: this.props.match.params.xxxx



要多传一个isMock参数来判断更改BaseApi



npm install redux —save

npm install react-redux —save

npm instal redux-devtools-extensions



antd必须要less less-loader bable-plugin-import 

然后在webpack.config中修改两处，一处是less-loader，一处是bable-plugin-import

less需要降级到2.7.3

npm install less@^2.7.3

基于cookie的验证`npm install cookie-parser --save`