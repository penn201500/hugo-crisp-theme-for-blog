+++
Categories = ["python"]
Description = "python奇思妙解"
Tags = ["python3"]
title = "python3 zip的用法"
comments = true
date = 2016-06-19T19:04:40Z
+++

---

* * *

## **例子：**

> 井字游戏，有时也被称为“进攻和防守”，是一个两人玩家（X和O）轮流标志着3×3的网格的空间的连珠游戏。最先在任意一条直线（水平线，垂直线或对角线）上成功连接三个标记的一方获胜。
> 
> 但我们不去玩这个游戏。你将是这个游戏的裁判。你被赋予游戏的结果，以及你必须判断游戏是平局还是有人胜出，以及谁将会成为最后的赢家。如果X玩家获胜，返回“X”。如果O玩家获胜，返回“O”。如果比赛是平局，返回“D”。
> 
> x-o-referee
> 
> 游戏的结果是作为字符串形式的列表，其中“X”和“O”是玩家的标志，“.”是空格。
> 
> **输入:** 游戏结果作为字符串形式的列表(Unicode)。
> 
> **输出:** “X”，“O”或“D”作为字符串形式。
> 
> **范例:**
> 
> checkio([
>     “X.O”,
>     “XX.”,
>     “XOO”]) == “X”
> 
> checkio([
>     “OO.”,
>     “XOX”,
>     “XOX”]) == “O”
> 
> checkio([
>     “OOX”,
>     “XXO”,
>     “OXX”]) == “D”
> 
> **如何使用：** 此任务中的概念将有助于您遍历数据类型。这还可以用在游戏的算法上，让你知道如何去检查结果。

**最多推荐的解法：**

    def checkio(result):
        rows = result
        cols = map(''.join, zip(*rows))
        diags = map(''.join, zip(*[(r[i], r[2 - i]) for i, r in enumerate(rows)]))
        lines = rows + list(cols) + list(diags)
    ​
        return 'X' if ('XXX' in lines) else 'O' if ('OOO' in lines) else 'D'

上面的最多推荐的解法，步骤是：

**1.将列表result中的3个元素拆开成3个tuple（tuple是列的元素组合）**

>\>>> result = [
> …     “OOX”,
> …     “XXO”,
> …     “OXX”]
> 
> \>>> rows = result
> 
> \>>> for i in zip(*rows):
> 
> …   print(i)
> 
> …
> 
> (‘O’, ‘X’, ‘O’)
> 
> (‘O’, ‘X’, ‘X’)
> 
> (‘X’, ‘O’, ‘X’)
> 
> \>>>

**2.获取对角线上的元素组合**

**3.行上的元素组合+列上的元素组合+对角线元素组合，然后判断胜利方**

## **zip的用法：**

    >help(zip)

    Help on class zip in module builtins:

    class zip(object)

     |  zip(iter1 [,iter2 [...]]) --> zip object
     |
     |  Return a zip object whose .__next__() method returns a tuple where
     |  the i-th element comes from the i-th iterable argument.  The .__next__()
     |  method continues until the shortest iterable in the argument sequence
     |  is exhausted and then it raises StopIteration.
     |
     |  Methods defined here:
     |
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |
     |  __iter__(self, /)
     |      Implement iter(self).
     |
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |
     |  __next__(self, /)
     |      Implement next(self).
     |
     |  __reduce__(...)
     |      Return state information for pickling.

zip输入参数是一些迭代器，执行完成之后返回zip object（迭代器 ,tuple list）。

**zip用法中需要注意的是：**

**1.zip是将每个可迭代对象的对应位置元素打包成一个tuple组，例如：**

    二维矩阵变换（矩阵的行列互换）
    比如我们有一个由列表描述的二维矩阵
    a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    利用zip函数：
    >>> a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    >>> zip(*a)
    [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
    >>> map(list,zip(*a))
    [[1, 4, 7], [2, 5, 8], [3, 6, 9]]

**2.(*)操作符与zip函数配合可以实现与zip相反的功能,即将合并的序列拆成多个tuple，如解法中的zip(*rows)。如：**

    >>>x=[1,2,3],y=['a','b','c']
    >>>zip(*zip(x,y))
    [(1,2,3),('a','b','c')]

**3.新的序列的长度以参数中最短的序列为准.**

    >>>x=[1,2],y=['a','b','c']
    >>>zip(x,y)
    [(1,'a'),(2,'b')]

**zip另有一些高级用法：****1.python列表相邻元素压缩：**

    group_adjacent = lambda a, k: zip(*([iter(a)] * k))

强烈推荐阅读：[https://segmentfault.com/q/1010000000612945](https://segmentfault.com/q/1010000000612945)

关键摘录：
iter() 能把一个序列生成为一个和迭代器，迭代器的特点是可以用 for in 语句迭代，原理是迭代器对象有一个next方法，可以每次移动迭代的指针，一旦迭代完，没有下一个元素的时候，会应发一个 StopIteration 异常。

迭代器的特点就是，迭代了一次之后，指针就移动了，不会自动回溯。例如可以用 for in 列表 a 无数次，却只能for in 迭代器 x 一次。

如果不用迭代器？

    >>> a = [1, 2, 3, 4, 5, 6]
    >>> x = iter(a)
    >>> t = [a, a]
    >>> zip(*t)                 # 1
    [(1, 1), (2, 2), (3, 3), (4, 4), (5, 5), (6, 6)]  
    >>> tx = [x, x]                                   
    >>> zip(*tx)                # 2
    [(1, 2), (3, 4), (5, 6)]
    >>> 

    #1 这里的含义表示zip 传了两个参数a，a1 a2 都是a，所以就打包了这两个序列。
    #2 这里面因为 x 是迭代器对象，迭代就调用 next 方法，之后就不会有了。也就是 zip 执行打包的过程先调用第一个参数的 x 的 next 方法得 1，然后调用第二个参数的 x 的next，因为这两个x对象实际上是一样的，调用第二个 x 的 next 方法的时候，迭代的指针已经移动，实际得到的时2，以次类推，过程模拟如下表示
         x.next -> 1
         x.next -> 2
         zip(x.next(), x.next()) ---> zip(1, 2)
         x.next -> 3
         x.next -> 4
         zip(x.next(), x.next()) ---> zip(3, 4)
        ....

等价于下面的方式

    zip([1, 3, 5], [2, 4, 6])

所以代码：

    group_adjacent = lambda a, k: zip(*([iter(a)] * k))

表示定义一个匿名函数，参数是 a和k，并绑定变量 group_adjacent。匿名函数的主体内容是，用iter将序列迭代化，然后用zip打包这个迭代器对象。

**2.使用zip反转字典**

    >>> m = {'a': 1, 'b': 2, 'c': 3, 'd': 4}
    >>> m.items()
    [('a', 1), ('c', 3), ('b', 2), ('d', 4)]
    >>> zip(m.values(), m.keys())
    [(1, 'a'), (3, 'c'), (2, 'b'), (4, 'd')]
    >>> mi = dict(zip(m.values(), m.keys()))
    >>> mi
    {1: 'a', 2: 'b', 3: 'c', 4: 'd'}

**3.使用zip和iterators生成滑动窗口 (n -grams)**

    >>> from itertools import islice
    >>> def n_grams(a, n):
    ...     z = (islice(a, i, None) for i in range(n))
    ...     return zip(*z)
    ...
    >>> a = [1, 2, 3, 4, 5, 6]
    >>> n_grams(a, 3)
    [(1, 2, 3), (2, 3, 4), (3, 4, 5), (4, 5, 6)]
    >>> n_grams(a, 2)
    [(1, 2), (2, 3), (3, 4), (4, 5), (5, 6)]
    >>> n_grams(a, 4)
    [(1, 2, 3, 4), (2, 3, 4, 5), (3, 4, 5, 6)]
    #
    islice的用法：
    islice()    seq, [start,] stop [, step] elements from seq[start:stop:step]  islice('ABCDEFG', 2, None) --> C D E F G
    测试islice：
    >>> a = [1, 2, 3, 4, 5, 6]
    >>> for x in islice(a,0,None):
    ...   print(x)
    ...
    1
    2
    3
    4
    5
    6
    >>> a = [1, 2, 3, 4, 5, 6]
    >>> for x in islice(a,1,None):
    ...   print(x)
    ...
    2
    3
    4
    5
    6
    >>> a = [1, 2, 3, 4, 5, 6]
    >>> for x in islice(a,2,None):
    ...   print(x)
    ...
    3
    4
    5
    6
    >>>

**注：**例题解法来自 [https://checkio.org/](https://checkio.org/)

我在 [https://checkio.org/user/penn201500/](https://checkio.org/user/penn201500/) ：）

* * *

**参考：**

[PYTHON-进阶-ITERTOOLS模块小结](http://wklken.me/posts/2013/08/20/python-extra-itertools.html)

[Python零碎知识(2):强大的zip](http://www.cnblogs.com/BeginMan/archive/2013/03/14/2959447.html)

[python列表相邻元素压缩器](https://segmentfault.com/q/1010000000612945)

* * *

