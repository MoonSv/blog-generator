---
title: Java
date: 2019-06-11 15:39:00
tags:
---

# 数据类型

1. 原生数据类型和引用数据类型(对象)

   - 原生数据类型永远是数据本身
   - 引用数据类型则储存地址

2. Java int的最大值是**21亿**，为什么要记住这个数字？因为像类似淘宝这类互联网企业的成交量很容易就会超过这个值

   Java的每个类型都有最大值和最小值，如果超出了这个值就会溢出，溢出是没有任何征兆和异常的

3. 浮点数是一个近似的表示，是不精确的。所以在Java中判断浮点数是否和某数值相等是不安全的

   ```java
   double d = 1.0
   // 这样是不安全的
   if (d == 1.0) {
     ...
   }
   // 这样是安全的
   if (Math.abs(d - 1.0) < 0.000001){
     ...
   }
   ```

4. 另外一个坑，整数除法是地板除

   ```java
   public double divide(int a, int b){
     return a / b;
   }
   
   psvm(){
     sout(divide(3, 2)) // Oops, result = 1.0
   }
   
   // 可以修改成
   public double divide(int a, int b){
     return 1.0 * a / b; // 这里会发生变量提升，提升到精度更高的级别
   }
   ```

5. 所有原生数字类型在声明时就会有默认的**初始值**，引用类型也有默认的**初始值**，值为null

   ```java
   int a; // -> int a = 0;
   double b; // -> double b = 0d;
   float c; // -> float c = 0f;
   
   String name; // -> String name = null;
   ```

# 对象

1. 对象的生命周期

## 访问控制符

- public 任何人都能访问
- protected 只有字类可以访问和同一个包的可以访问
- package private 只有同一个包的类可以访问
- private 只有自己可以访问

# 设计者模式

## 静态工厂设计模式

1. 最重要的特征和优点是静态工厂构造器可以是**有名字**的，即可以通过名字来判断改构造方法是做什么的

   ```java
   public static Cat newCuteCat(String name){
     // 第一个参数是名字，那二个布尔参数表示是否是萌猫
     return new Cat(name, true)
   }
   ```

2. 可以返回当前声明类型的**子类型**

3. 如果使用静态工厂方法代替构造器，就先将***原有构造器私有化***（让所有人必须通过静态工厂来创建对象，实际上是一个**封装**的表现）

## Builder 模式

有时一个类可能有成百上千个参数，所以当构造这个类的时候会因为参数太多而不知道所传入的参数对应的是什么，造成参数的误传。这个时候就可以使用builder模式

```java
public class UserBuilder {
    private String firstName;
    private String lastName;
    private String phoneNumber;
    private String address;
    public UserBuilder firstName(String firstName){
        this.firstName = firstName;
        return this;
    }
    public UserBuilder lastName(String lastName){
        this.lastName = lastName;
        return this;
    }
    public UserBuilder phoneNumber(String phoneNumber){
        this.phoneNumber = phoneNumber;
        return this;
    }
    public UserBuilder address(String address){
        this.address = address;
        return this;
    }
    public User build(){
        return new User(firstName, lastName, phoneNumber, address);
    }
}
```

Builder可以使用`command + n`来自动构建

# 继承

继承的本质是避免重复

## .equals()

因为每个类都会单边继承`Object`类，所以每个类会拥有Object类中的`.equals()`方法

# 多态

- 实例方法默认是多态的
  - 在运行时根据this来决定调用哪个方法
  - **静态方法没有多态**
  - 参数静态绑定，接受者动态绑定
    - 换句话说，多态只对方法的接受者生效

# 抽象类

- 不可实例化
- 可以实例化的东西一定要补全所有方法体
- 可以包含抽象方法 - 非private/static
- 可以包含普通类的任何东西

# 命令行

- 单引号内为原样输出

- 双引号则会识别$

- 在Java中如果想获取环境变量：`System.getEnv()`

- 在Java中如果想获取系统属性: `System.getProperty()`

- **java -D参数可以向jvm中传递一些数据**

- 输出

  - 标准输出默认为1号输出

    ```shell
    java Main > output.txt 
    java Main 1 > output.txt
    二者等价
    ```

  - 标准错误默认为2号输出