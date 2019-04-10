---
title: Java修饰符
date: 2018-12-21 22:22:15
tags:
---

修饰符用于控制变量，类的作用与喝一些访问限制

1. 访问权限修饰符： `public`, `protected`, `private`, `default(即不设置)`

   一般把成员变量设置为`private`，用`get`和`set`函数去访问修改这个成员变量

|          | public | protected | default | private |
| -------- | ------ | --------- | ------- | ------- |
| 同一个类 | Y      | Y         | Y       | Y       |
| 同一个包 | Y      | Y         | Y       |         |
| 子父类   | Y      | Y         |         |         |
| 不同包   | Y      |           |         |         |

2. `static`: 把方法或者成员变量设置为类共享

具有`static`修饰的方法和变量的类，我们称之为“静态类”

调用方法：<类名>.<方法名或成员变量名>

```java
public class Main{
    public static void main(String[] args){
        System.out.println("Hello, world")
    }
}
// 调用：
Main.main(null)
```

3. `final`
   - `final<类>;` —防止类被继承
   - `final<变量>;` —防止变量被修改引用到另外一个对象，可称为“常量”
     - 思考： 常量指向的**对象**能否被修改？
     - 是可以的，因为它只是防止修改引用
   - `final<方法>;` —防止方法被重载
   - `final`成员变量必须在生命时候初始化，或者在构造函数中初始化！！