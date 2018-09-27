---
title: React-2
date: 2018-08-14 16:19:35
tags:
---
#### 关于JSX语法的注意事项
1. 在JSX中写注释：推荐使用`{/* this is the comment */}`
2. 在JSX中的元素添加**class**类名需要使用`className`来代替`class`; `htmlFor`替代**label**的`for`属性
3. 在JSX创建DOM的手，所有的节点必须有**唯一**的根元素进行包裹
4. 在JSX语法中，标签必须成对出现，如果是单标签则必须**自闭和**

##### React创建组件
1.使用构造函数来创建组件，如果要接受外界传递的数据，需要在构造函数的参数列表中使用`props`来接收；必须要向外return一个合法的JSX创建的虚拟DOM

```jsx
// 第一种创建组件的方式，一个普通的构造函数就是组件(构造函数特点是首字母大写)
function Hello() {
    // 如果在一个组件中return一个null，则表示次组件是空的，什么都不渲染
    return <div>Hello</div>;
}

// 使用ReactDOM把虚拟DOM渲染到页面上
ReactDOM.render(
    <div>
        {/*直接把组件的名称以标签的形式丢到页面上即可*/}
        <Hello></Hello>
    </div>,
    document.getElementById('app'));
```

* 为组件传递props数据
    ```jsx
    function Hello(props) {
        // 如果在一个组件中return一个null，则表示次组件是空的，什么都不渲染
        console.log(props);
        return <div>Hello {props.name}!</div>;
    }

    let dude = {
        "name": "Roger",
        "gender": "male"
    }

    // 使用ReactDOM把虚拟DOM渲染到页面上
    ReactDOM.render(
        <div>
            {/*直接把组件的名称以标签的形式丢到页面上即可*/}
            <Hello {...dude}></Hello>
        </div>,
        document.getElementById('app'));
    ```

* 为了符合组件化开发思想，应将组件放入外部文件中。如创建一个``Hello.jsx`文件
    ```jsx
    import React from 'react'
    // 一定要先导入React

    export default function Hello(props) {
        // 如果在一个组件中return一个null，则表示次组件是空的，什么都不渲染
        console.log(props);
        return <div>Hello {props.name}!</div>;
    }
    ```
    然后在`js`文件中导入`Hello`组件即可`import Hello from './components/Hello.jsx'`
* 我们也可以在`webpack.config.js`配置文件中的导出对象中配置`resolve`来免去写后缀名
```
resolve: {
        extensions: ['.js', '.jsx', '.json'] 
        // 表示这几个文件的后缀名可以省略不写
}
```
* 配置webpack设置根目录，依然是在`webpack.config.js`配置文件中的导出对象中配置`resolve`设置
```jsx
    resolve: {
        extensions: ['.js', '.jsx', '.json'], 
        // 表示这几个文件的后缀名可以省略不写
        alias: {
            '@': path.join(__dirname, './src') 
            // 这样，@就表示项目跟目录中src这一层路径
        }
    }
```

1. 使用class关键字来创建组件

    **了解ES6中class关键字的使用**
    * 使用class创建类及构造函数的使用

        ```js
        class Animal {
        // 如果没有指定构造器，则默认有一个无参构造器
            constructor(name, age) {
                this.name = name;
                this.age = age;
            }
        }

        const a1 = new Animal('dolphin', 13);
        console.log(a1);
        ```
    * 使用`static`创建**静态属性**
    > 通过构造函数直接访问到的属性，叫做**静态属性**

    ```js
    // 在class内部，通过static修饰的属性就是静态属性
    static info = 'eee';
    consolo.log(Animal.info); // 直接调用静态属性
    ```

    * 实例方法和静态方法

        ```js
        // 这是动物的实例方法
        run(){
            console.log('run!')
        }
        //这是动物的静态方法
        static fly() {
            console.log("fly!");
        }
        ```

    * class继承extends

        ```js
        // 父类
        class Person{
            constructor(name, age) {
                this.name = name;
                this.age = age;
            }
            sayHello(){
                console.log("Hi!")
            }
        }
        // 在class类中，可以使用extends关键字实现子类继承父类
        class Programmer extends Person{
            constructor(name, age){
                //如果一个子类通过`extends`关键字继承了父类，那么在子类的`constructor`构造函数中，必须优先调用一下`super()`
                super(name, age);
            }
            code() {
                console.log("coding...");
            }
        }
        const a1 = new Programmer('Joe', 13);
        console.log(a1);
        class Designer extends Person{
            draw() {
                console.log("drawing...")
            }
        }
        const a2 = new Designer('Zoe', 11);
        console.log(a2);
        a2.sayHello()

        ```

        * 如果一个子类通过`extends`关键字继承了父类，那么在子类的`constructor`构造函数中，必须优先调用一下`super()`
        * `super()`是一个函数，即父类的构造器。子类中的`super()`其实就是父类中`constructor`构造器的一个引用
        * 规定在子类中`this`只能放到`super()`之后，来创建该子类独有的属性

    **基于class关键字创建组件**
    1. 最基本的组件结构：

        ```jsx
        // 如果要使用class定义组件必须让自己的组件继承自React.component
        class 组件名称 extends React.Component {
            // 在组件内部，必须有render函数
            render(){
            // render函数中必须返回合法的JSX虚拟DOM结构
            return <div>这是class创建的组件</div>
        }
        ```
        实例：
        ```jsx
        class Movie extends React.Component {
            // render函数作用：渲染当前组件所对应的虚拟DOM元素
            render(){
                return <div>Harry Potter<br/>
                    {this.props.name}
                    {this.props.age}
                    </div>
            }
        }

        const user = {
            name: "Joe",
            age: 12,
        }

        ReactDOM.render(
            // 传参方式
            <Movie {...user}></Movie>,
            document.getElementById('app'));
        ```

    2. state
        * props的数据都是只读的，可以通过在构造器里创建state属性，该属性是可读可写的。

        ```jsx
            constructor(){
                super();
                this.state = {
                    msg: 'wow!'
                }
            }
            
                // render函数作用：渲染当前组件所对应的虚拟DOM元素
            render(){
                this.state.msg = 'Wonderful'
                return <div>Harry Potter<br/>
                    {this.props.name}
                    {this.props.age}
                    <hr/>
                    {this.state.msg}
                    </div>
                }
            }
        ```


    **两种创建组件方式的对比**
    1. 使用class关键字创建的组件，有自己的私有数据`this.state`和生命周期函数；使用function创建的组件，只有props，没有自己的私有数据和生命周期函数
    2. 用**构造函数**创建出来的组件叫做**无状态组件**
    3. 用c**lass关键字**创建出来的组件叫做**有状态组件**(用的最多)
    4. `props`和`state`之间的区别
        + props中的数据都是外界传递过来的
        + state中的数据都是组件私有的（**通过Ajax获取回来的数据一般都是私有数据**）
        + props只读，state数据可读可写