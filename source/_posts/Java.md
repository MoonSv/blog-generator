---
title: Java
date: 2019-06-11 15:39:00
tags:
---

1. 数据类型

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

2. 逻辑运算符和短路特性

   ```java
   Boolean config = getConfig();
   // 1. config = true ->  true
   // 2. config = false -> false
   // 3. config = null -> 直接短路 -> false
   // 在这里运用短路特性，避免报错
   if (config != null && config){
     ...
   }
   ```

3. 三元运算符判断多个条件(嵌套)

   ```java
   int a = 1;
   int b = 2;
   /*
   * a > b -> return 1
   * a < b -> return -1
   * a == b -> return 0
   */
   int result = a > b ? 1 :(a < b ? -1 : 0)
   ```

   