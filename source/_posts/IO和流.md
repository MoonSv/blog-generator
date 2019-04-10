---
title: IO和流
date: 2018-12-23 11:53:30
tags:
---

I/O和流

- I/O是Input和Output的缩写
- 从读写设备，包括硬盘文件，内存，键盘输入，屏幕输出，网路
- 输入输出“内容”（字节或文本）
- 流是对输入输出设备的一种**抽象**
- 从流中读取内容，输出内容到流中
- “Linux中一切都是文件”
- 从程序的角度，就是对读写设备进行封装，比如：创建一个对象，然后调用方法读取（输出）内容，然后对象会更新当前文件的位置

标准输出流

- `System.out;`
- `System.out.println(...);`

标准输入流

- `System.in`

字节流

- `InputStream`
  - `System.in`
  - `FileInputStream`
- `OutputStream`
  - `System.out`
  - `FileOutputStream`
- `BufferedInputStream`和`BufferedOutputStream`
- `Stream`用于直接处理**“字节”**

字符流

- `Reader`
  - `InputStreamReader`
    - `FileReader`
  - `BufferedReader`
    - `bufferedReader.readline();`
- `Writer`
  - `OutputStreamWriter`
    - `FileWriter`
  - `BufferedWriter`
    - `bufferedWriter.write(String);`

IOUtils

- IOUtils是Apache开源项目的一个很广泛使用的IO工具库
- 主要提供更抽象程度IO放翁红菊，方便些IO相关的代码
- 常用类
  - FileUtils
  - Charset
  - DirectoryWalker
  - copyUtils

