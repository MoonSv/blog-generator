---
title: React-3
date: 2018-08-16 14:40:16
tags:
---

#### 使用CSS样式表美化组件

##### 操作步骤

1. 安装插件`npm i style-loader css-loader -D`

2. 在`webpack.config.js`中配置

   ```js
   module: { // 所有第三方模块配置的规则
     rules: [ // 第三方匹配规则
       {test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/},
       // 千万别忘记添加exclude排除项,否则会报错
       {test: /\.css$/, use: ['style-loader', 'css-loader']}, //打包处理css样式表的第三方loader
     ]
   },
   ```

3. 编写`.css`文件

4. 在组件文件中导入`import cssobj from '@/css/cmtlist.css'`，但`css`样式表是在全局生效的

5. 在要加样式的地方加入样式即可，例如`<h1 className=xxx></h1>`

##### 问题

1. 样式表是全局生效的()

   > 我们可以通过在`webpack.config.js`中module中给`css-loader`通过`?`加参数`modules`是样式模块化。操作前`console.log(cssobj)`是空值，操作后启用模块化则显示值

   css模块化只针对类选择器和Id选择器，并不会将标签选择器模块化

   解决：

   1. 启用css-modules

   - 修改`webpack.config.js`配置文件，为`css-loader`添加参数：

     ```js
     {test: /\.css$/, use: ['style-loader', 'css-loader?modules']},
     ```

   - 在需要的组件中，`import`导入样式表，并接受模块化的CSS样式对象

     ```jsx
     import cssObj from '@/css/cmtList.css'
     ```


-    在需要的HTML标签上，使用`className`指定模块化的样式

     ```jsx
     <h1 className={cssobj.title}>Hello, World!</h1>
     ```

   2. 使用`localIdentName`自定义生成的类名格式，可选的参数有：

   - [path]表示样式表`相对于项目根路径`的所在路径
   - [name]表示样式表文件名称
   - [local]表示样式的类名定义名称
   - [hash:length]表示32位的hash值
   - 例子：`test: /\.css$/, use: ['style-loader', 'css-loader?modules&localIdentName=[path][name]-[local]-[hash:5]']`
   3. 被`:global()`包裹起来的类名，不会被模块化，而是会全局生效

#### React中绑定事件的注意点

1. 事件的名称都是React提供的，因此名称的首字母必须是大写`onClick`、`onMouseOver`

2. 为事件提供的处理函数，必须是如下格式

   `onClick = { function }`

3. 用的最多的时间绑定形式为：

   ```jsx
   export default class BindEvent extends React.Component{
       constructor(){
           super();
           this.state = {}
       }

       render(){
           return <div>
               BindEvent组件
               <hr/>
               {/*在React中，有一套自己的事件绑定机制; 事件名使用驼峰命名*/}
               <button onClick={ () => this.myClickFunction() }>按钮</button>
           </div>
       }

       myClickFunction(){
           console.log('Test for click function.')
       }
   }
   ```

4. 在React中，如果想为state中的数据重新复制，不要使用this.state.xxx = value。而应该调用React中提供的this.setState({ msg: '123' })

   1. 在setState方法中，只会把对应的state状态更新，而不会覆盖掉其他的state状态
   2. this.setState方法是异步执行的，如果在调用玩this.setState之后又想立即拿到最新的state值，需要使用this.setState({}, callback)