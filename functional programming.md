# Functional Programming

+ 函数式编程，又称函数式设计，将计算机运算视为数学上函数计算，避免使用程序状态和易变对象。

+ 常见的函数式编程的函数：lambda，map，reduce，filter

+ lambda

 > > > f = lambda x : x + 2  # 定义函数 f(x) = x + 2
 > > >
 > > > g = lambda x, y : x + y  # 定义函数 g(x, y) = x + y

+ map
>>>map(function, iterable, ...)，function 指函数，iterable指一个或多个序列。
>>>
>>>Python 2.x 返回列表，Python 3.x 返回迭代器。
>>>
>>>```python3
>>>def pow(x):
>>>    return x**2
>>>ls1 = [1,2,3]
>>>ss = map(pow, ls1)
>>>print(ss)	# <map object at 0x00000070028FD198>，想要输出值：list(ss)，[1, 4, 9]
>>>```
>>>
>>>```python3
>>>ls1 = [1,2,3]
>>>s2 = map(lambda x : 2 + x, ls1)
>>>print(list(s2))		# [3, 4, 5]
>>>```

+ reduce
>>> reduce(function, iterable[, initializer])
>>> reduce() 函数会对参数序列中元素进行累积。
>>> 将传给 reduce 中的函数 function（有两个参数）的集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。
>>>
>>> ```
>>> from functools import reduce
>>> def add(x, y):
>>>     return x + y
>>> ls1 = [1,2,3]
>>> s3 = reduce(add, ls1)
>>> s4 = reduce(lambda x,y: x+y, ls1)
>>> print(s3)	# 6
>>> print(s4)	# 6
>>> ```

+ filter
>>> filter(function, iterable)
>>> 过滤器，筛选出符合条件的元素
>>>
>>> ```python3
>>> def is_odd(n):
>>>     return n % 2 == 1
>>> ls2 = range(1,10)
>>> s5 = filter(is_odd, ls2)
>>> print(list(s5))		# [1, 3, 5, 7, 9]
>>> ```


