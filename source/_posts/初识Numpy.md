---
title: 初识Numpy
date: 2018-02-01 11:22:12
tags:
---
# Numpy初识

1. 初级代码

    ```python
    import numpy as np
    
    np.zeros((2,3)) #zeros里必须是元组，默认格式为float, （2,3）是指生成2行3列的矩阵
    """
        array([[ 0.,  0.,  0.],
            [ 0.,  0.,  0.]])
    """
    np.zeros((2,3), dtype = np.int32) #将格式改为int
    """
        array([[0, 0, 0],
            [0, 0, 0]], dtype=int32)
    """
    np.random.random((2,3)) #生成2行3列的随机矩阵(随机数0-1)
    """
        array([[ 0.12901254,  0.40726237,  0.0391579 ],
            [ 0.69569515,  0.06916377,  0.26499276]])
    """
    np.linspace(1, 100, 100) #生成从1到100的100个数（平均分布）
    
    np.arange(15) #生成从0-14的单行矩阵
    np.arange(15).reshape(2,3) #将矩阵改为2行3列 
    
    ```
2. 一个易忽略的易错点
    
    ```python
    a = arange(12)
    b = a
    b.shape = 3,4
    # 这时a的shape也会被改变成(3,4)，这时因为a和b都指向了同一个值，只是那个值的两个不同的名字而已
    
    # 浅复制功能 view()   不推荐使用
    c = a.view()
    c[0,4] = 1234 # 这一步也会改变a[0,4]的值
    
    # 推荐使用 copy()
    d = a.copy()
    d[0,0] = 9999 # 这一步不会改变a[0,0]的值
    ```
3. 找矩阵每列最大值
    
    ```python
    data = np.sin(np.arange(15).reshape(3,5))
    index = np.argmax(axis = 0)
    data_max = data[index, range(data.shape[1])]
    ```
    
    `    np.argmax(axis = 0)表示取出每一列最大值的index
    在最后一行代码中，index是一个包含每一列最大值的index的list；data.shape是(3,5)，所以data.shape[1]值为5也就是表示该矩阵一共有五列，所以用range函数可以和index一一对应取该列的最大值`


