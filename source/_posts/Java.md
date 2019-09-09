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
- `Collections.sort()`可以用来在自定义排序算法之后进行排序

# 接口

- 在Java8中，接口里可以写static和default方法

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
  
  - ```shell
    java Main 1 > output.txt 2>&1
    ```

# Maven

- Maven会把一些包提前下载至.m2文件夹下，方便使用

- 常见的**包冲突**error：

  1. `AbstractMethodError`
  2. `NoClassDefFoundError`
  3. `ClassNotFoundError`
  4. `LinkageError`

- 传递性依赖的自动管理

  - 原则：绝对不允许最终的classpath出现同名不同版本的jar包

- 依赖冲突的解决：原则：最近的胜出

- 可以用

  ```SHELL
  mvn dependency:tree
  ```

  来获取依赖的信息

- intellj安装插件maven helper

- maven scope用来定义包在什么位置有效，例如如果scope为test就代表只在test下会引入这个包，而在main下不会引入，从而实现依赖的隔离

  compile: 可以理解为main和test都会引入

  provided: 只在编译的时候有效，运行的时候就没有效果了

  - 标准错误默认为2号输出

# Collection

1. **ArrayList**

   - ArrayList可以使用构造器将任意一个collection传入形成一个新的ArrayList，这个ArrayList里面包含这个collection的所有元素

     ```java
     Collection<Integer> c = new LinkedHashMap();
     
     // IntegerList
     List<Integer> list = new ArrayList<>(c);
     
     // 等价于
     List<Integer> list2 = new ArrayList<>();
     list2.addAll(c);
     
     // 等价于
     List<Integer> list3 = new ArrayList<>();
     for (Integer i: c){
       list3.add(i);
     }
     ```

2. HashSet是无序的(完全随机)，如果有需要可以使用LinkedHashSet(按插入顺序排序)

3. Map

   - C/U: put() / putAll()

   - R:

     - get() / size()

     - containsKey() / containsValue()

     - keySet() / values() / entrySet()

       **Map本身和这几个是双向绑定的，即改变其中一个会影响改变另一个**

       values是可以重复的所以返回的是一个**Collection**

       entrySet()是一个键值对的集合

       ```java
       for (Map.Entry<String, String> entry : map.entrySet()){
       	System.out.println(entry.getKey());
         	System.out.println(entry.getValue());
       }
       ```

       

   - D: remove() / clean()

   - TreeSet最大特点是它是一个**有序**集合

   - 面试题
   
     - 请说一下HashMap扩容的过程
     - HashMap线程不安全，要用ConcurrentHashMap
     - HashMap在jdk7+改变
     
   - Collections工具方法集合
   
     - emptySet(): 返回一个方便的空集合
     - synchronizedCollection: 将一个集合编程线程安全的
     - Unmodifieablecollection: 将一个集合编程不可变的（也可以使用Guava的Immutable）
   
   - Guava
   
     - 不要重复发明轮子！尽量使用经过实战检验的类库
     - Lists/Sets/Maps
     - ImmutableMap/ImmutableSet
     - MultiSet/MultiMap
     - BiMap
     - MultiSet使用静态工厂方法
       - 回忆静态工厂方法，一定有一个private的构造器，来确保要想构建实例只能通过静态工厂方法来返回
     - MultiMap, 一个key可以对应多个value

# 文件与IO

1. File

   - File是一个路径
   - `file.getCanonicalPath()`将复杂的目录关系简单整理化

2. NIO

   - Java7之后引入的
   - New IO / Non-blocking IO
   - NIO的Path就是旧版本的File
   - Java7引入了Files
     - 如果一个名字代表一个类的话，那么其s方法（如Files）就代表该类的工具方法集合
     - `Files.readAllLines(Path path)`是一个常用的方法，用于不想使用第三方库的时候

3. 练习

   很多种方式来实现IO

   1. Commons.IO中的FileUtils

      ```java
      // read file
      FileUtils.readlins(file); // File file
      
      // write into file
      FileUtils.writelines(lines) // List<String> lines
      ```

   2. BufferedReader & BufferedWriter

      ```java
      // read file
      public static List<String> readFile2(File file) {
        BufferedReader bufferedReader = null;
        List<String> lines = new ArrayList<String>();
        try {
          bufferedReader = new BufferedReader(new FileReader(file));
          String line;
          while ((line = bufferedReader.readLine()) != null) {
            lines.add(line);
          }
      
        } catch (IOException e) {
          e.printStackTrace();
        } finally {
          try {
            bufferedReader.close();
          } catch (IOException e) {
            e.printStackTrace();
          }
        }
        return lines;
      }
      
      // write into file
      public static void writeLinesToFile2(List<String> lines, File file) {
        BufferedWriter bufferedWriter = null;
        try {
          bufferedWriter = new BufferedWriter(new FileWriter(file));
          for (String s : lines
              ) {
            bufferedWriter.write(s);
            bufferedWriter.newLine(); // indicate there is a newline
          }
        } catch (IOException e) {
          e.printStackTrace();
        } finally {
          try {
            bufferedWriter.close();
          } catch (IOException e) {
            e.printStackTrace();
          }
        }
      }
      ```

   3. Files工具类

      ```java
      // read file
      public static List<String> readFile3(File file) throws IOException {
        return Files.readAllLines(Paths.get(file.getPath()));
      }
      
      // write into file
      public static void writeLinesToFile3(List<String> lines, File file) throws IOException {
        Files.write(Paths.get(file.getPath()), lines);
      }
      ```

# 异常

1. `try/catch/finally`

   1. 如果没有try，异常将击穿所有的栈帧

   2. catch可以将一个异常抓住

   3. finally执行清理工作

   4. JDK7+: try-with-resources

      只要是实现了`Closable`的类都可以使用try-with-resources

2. throw / throws

   - throw指直接抛出一个异常，写在代码块里
   - throws指这个**方法**有可能会抛出一个异常

   15502299857

3. Throwable - 可以被抛出的东西（有毒）

   1. Exception - checked exception (受检异常，有毒， 代表一种预料之中的异常，IOException)

      RuntimeException (运行时异常，无毒， 代表一种预料之外的异常，因此不需要声明)

   2. Error (错误，毒)

## 异常的抛出原则

1. 能用`if/else`处理的，不要使用异常

2. 尽早抛出准异常

3. 异常要准确，带有详细信息

4. 抛出异常也比悄悄执行错误的逻辑强的多

5. 本方法是否有责任处理这个异常？

   不要处理不归自己管的异常

6. 本方法是否有能力处理这个异常

   如果自己无法处理，就抛出

7. 如非万分必要，不要忽略异常

# 多线程

## 查看程序的执行时间

```java
long t0 = System.currentTimeMillis();
function();
long t1 = System.currentTimeMillis();
System.out.println("runs" + (t1 - t0) + "ms"); 
```

## Thread

- Java中只有这么一种东西代表线程
- `start`方法才能并发执行！
- 每多开一个线程，就多个执行流
- 方法栈（局部变量）是**线程私有**的
- 静态变量/类变量是被**所有线程共享**的

## 多线程的使用场景

- 对于IO密集型应用极其有用
  - 网路IO（通常包括数据库）
  - 文件IO
- 对于CPU密集型应用稍有折扣
- 性能提升的上限在哪里？
  - 单核CPU：100%
  - 多核CPU：N * 100%

## 线程不安全的表现

- 数据错误
  - `i++`
  - `if-then-do`
- 著名的HashMap的死循环问题
- 写一段代码来重现死锁
- 预防死锁产生的原则：
  - 所有的线程都按照相同的顺序获得资源的锁
- 死锁问题的排查
- 多线程的经典问题：哲学家用餐

## 线程安全

