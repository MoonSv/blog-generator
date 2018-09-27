---
title: React-1
date: 2018-08-14 00:18:43
tags:
---

#### React 简介
- React 是一个用于构建用户界面的渐进式 JavaScript 库
  - 本身只处理 UI
  - 不关系路由
  - 不处理 Ajax
- React主要用于构建UI，很多人认为 React 是 MVC 中的 V（视图）。
  - 数据驱动视图
- React 由 Facebook 开发
- 第一个真生意义上把组件化思想待到前端开发领域
  - Angular 早期没有组件化思想
  - 后来也被 Vue 学习借鉴了

  
#### 虚拟DOM(Virtual Document Object Model)
- DOM的本质是什么：浏览器中的概念，用JS对象来表示页面上的元素，并提供了操作DOM对象的API；
- 什么是React中的虚拟DOM：用JS对象来模拟页面上的DOM和DOM嵌套
- 虚拟DOM的目的(意义)：为了实现页面中DOM元素的高效更新

> 在开发的时候，为了将数据实时的显示在页面上，就需要对DOM进行操作，但是复杂或者频繁的DOM操作通常都是性能瓶颈产生的原因。所以react引用了虚拟DOM这一机制，就是说react只是将元素存在缓存中，虚拟DOM通过高效的diff算法只会对页面上真正变化的部分进行实际的DOM操作。

#### 创建基本的webpack项目
1. 运行`npm init -y`快速初始化项目
2. 在项目根目录创建`src`源代码目录和`dist`产品目录
3. 在`src`目录下创建`index.html`
4. 使用`npm`安装webpack，指令为`npm i webpack -D`
    * 全局安装：`npm i webpack -g`
5. 创建webpack的配置文件`webpack.config.js`，注意webpack 4.x 提供了约定大于配置的概念，目的是为了尽量减少配置文件的体积
    * 默认约定了打包的入口是`src` -> `index.js`
    * 打包的输出文件是`dist` -> `main`
    * 4.x中新增了`mode`选项(为必选项)，可选的值为`development`和`production`
    * ```
    module.exports = {
    mode: "development"
};```

#### 第一个React代码

```js
import React from 'react' // 创建组件、虚拟DOM元素，生命周期
import ReactDOM from 'react-dom' // 把创建好的组件和虚拟DOM放在页面上展示


// 2. 创建虚拟DOM元素
// 参数1： 创建的元素的类型，字符串，表示元素的名称
// 参数2： 是一个对象或null，表示当前这个DOM的属性
// 参数3： 子节点（包括其他虚拟DOM 获取 文本子节点）
// 参数n： 其他子节点
// <h1 id="myh1" title="this is a h1">Yes!<h1>
const myh1 = React.createElement('h1', {id: 'myh1', title:'this is a h1'}, "Yes!");

const mydiv = React.createElement('div', null, 'This is a div', myh1);

// 渲染页面上 DOM 的最好方式就是写html代码



// 3. 使用ReactDOM把虚拟DOM渲染到页面上
// 参数1： 要渲染的那个虚拟DOM元素
// 参数2： 指定页面上的一个容器
ReactDOM.render(mydiv, document.getElementById('app'));
```
#### JSX
* 通过上述代码可以看出，如果要生成很多的HTML代码操作将会变得比较麻烦，而渲染页面上DOM的最好方式就是写HTML代码，所以引入了JSX语法：

> 在JS中混合写入类似于HTML的语法，叫做JSX语法(X代表符合XML规范)，使用babel将这种HTML写法转换成上述代码形式

* 注意：JSX语法的本质还是在运行的时候，将HTML代码形式转换成React.createElement形式来执行的
* 如何启用JSX语法?
    * 安装`babel`插件
        * 运行`npm i babel-core babel-loader babel-plugin-transform-runtime -D`
        * 运行`npm i babel-preset-env babel-preset-stage-0 -D`
    * 安装能够识别JSX语法的包`babel-preset-react`
        * 运行`npm i babel-preset-react -D`
    * 在项目根目录中创建名为`.babelrc`的配置文件

    ```javascript
    {
        "presets": ["env", "stage-0", "react"],
        "plugins": ["transform-runtime"]
    }
    ```
    * 在`webpack.config.js`配置文件中配置第三方loader

    ```js
    // webpack默认只能打包处理.js后缀名类型的文件，像.png .vue无法主动处理
    // 所以要配置第三方的loader规则
    module.exports = {
        mode: "development",
        plugins: [
            htmlPlugin
        ],
        module: { // 所有第三方模块配置的规则
            rules: [ // 第三方匹配规则
                {test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/},
                // 千万别忘记添加exclude排除项，否则会报错
            ]
        }
    };
    ```
    * 一切配置完成后，就可以在.js文件中使用JSX语法了
    
    ```jsx
    const mydiv = <div id="mydiv" title="div aaa">
    This is a div element
    <h1>Rick and Morty</h1>
    </div>
    
    ReactDOM.render(mydiv, document.getElementById('app'));
    ```
    
* 实例：将普通字符串数组，转换成JSX数组并渲染到页面上
    * 注意：React中，需要把key添加给被forEach, map或for循环直接控制的元素

```JSX
const names = ['love🍌', 'love🍊', 'dislike🍐'];
```
```JSX
// 方案一： 定义一个空数组，将来用来存放名称及标签
const nameArr = [];
names.forEach(item => {
    const tmp = <h5 key={item}>{item}</h5>;
    nameArr.push(tmp);
})

// 使用ReactDOM把虚拟DOM渲染到页面上
ReactDOM.render(
    nameArr,
    document.getElementById('app'));
```
```JSX
// 方案二: 用.map方法在内部编写(map一定要有return)
ReactDOM.render(
    <div>
    {names.map(item => {
        return <h5 key={item}>{item}</h5>
    })}
    </div>,
    document.getElementById("app")
)
```
如果箭头函数只有一行代码，则可以省略大括号，如果大括号省略则return也可以不必填写。则可以简写成
```JSX
ReactDOM.render(
    <div>
    {names.map(item => <h5>{item}</h5>)}
    </div>,
    document.getElementById("app")
)
```
        



