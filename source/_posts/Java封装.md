---
title: Java封装
date: 2018-12-25 14:12:12
tags:
---

### 封装

- 在面向对象程序设计方法中，封装（Encapsulation）是指一种将类实现细节部分包装，隐藏起来的方法
- 目的：**对类的内部状态的访问进行控制，只提供该提供的信息**
- 把代码分成两个部分：**接口**和**实现**
- 接口因为涉及和外部的交互，对用户暴露，**应该保持稳定**。例如API和库
- 内部实现不需要暴露给外部用户，在街口功能不被影响的前提下，可以随意修改和重构
- 良好的封装是解耦的基础！

### 继承

继承是Java面向对象编程技术的一块基石，因为它允许创建分等级层次的类封装方式：类

子类继承父类的特征和行为，使得子类对象具有父类对象的特征和方法

继承需要符合一个关系：is-a.子类是更具体的父类

在声明子类的时候，通过关键字`extends`表达继承

- 继承特性

  - 子类拥有父类非private的成员变量和方法
  - 子类可以拥有有自己的成员变量和方法，即子类可以对父类进行扩展
  - 子类可以重新实现此类的方法，`override`
  - Java只支持单继承，即只能有一个父类
  - super关键字：我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类
  - this关键字：指向自己的引用

- 构造方法

  - 子类不能继承父类的构造器（构造方法或者构造函数），如果父类的构造器带有参数，则必须在子类的构造器中显式地通过super关键字调用父类的构造器并配以适当的参数列表。
  - 如果父类构造器没有参数，则在子类的构造器中不需要使用super关键字调用父类构造器，系统会自动调用父类的无参构造器

- 举例

  - 父类

    ```java
    public class Father {
        protected String name;
        protected int age;
        Father(){
        }
        Father(String name, int age){
            this.name = name;
            this.age = age;
        }
        public void eat(String food){
            System.out.println(this.name + " is eating " + food);
        }
    }
    ```

  - 子类

    ```java
    public class Child extends Father{
        Child(){
            super();
        }
        Child(String name, int age){
            super(name, age);
        }
        @Override
        public void eat(String food){
            System.out.println(this.name + " is plan to eat " + food);
        }
    }
    ```
