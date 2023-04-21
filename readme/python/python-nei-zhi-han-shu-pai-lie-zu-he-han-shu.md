# python内置函数-排列组合函数

product 笛卡尔积　　（有放回抽样排列）

permutations 排列　　（不放回抽样排列）

combinations 组合,没有重复　　（不放回抽样组合）

combinations\_with\_replacement 组合,有重复　　（有放回抽样组合）

详细的参见官网。

```
>>> import itertools
>>> for i in itertools.product('ABCD', repeat = 2):
...     print(i)
...
('A', 'A') ('A', 'B') ('A', 'C') ('A', 'D') ('B', 'A') ('B', 'B') ('B', 'C') ('B', 'D') ('C', 'A') ('C', 'B') ('C', 'C') ('C', 'D') ('D', 'A') ('D', 'B') ('D', 'C') ('D', 'D')
>>> for i in itertools.permutations('ABCD', 2):
...     print(i)
...
('A', 'B') ('A', 'C') ('A', 'D') ('B', 'A') ('B', 'C') ('B', 'D') ('C', 'A') ('C', 'B') ('C', 'D') ('D', 'A') ('D', 'B') ('D', 'C')
>>> for i in itertools.combinations('ABCD', 2):
...     print(i)
...
('A', 'B') ('A', 'C') ('A', 'D') ('B', 'C') ('B', 'D') ('C', 'D')
>>> for i in itertools.combinations_with_replacement('ABCD', 2):
...     print(i)
...
('A', 'A') ('A', 'B') ('A', 'C') ('A', 'D') ('B', 'B') ('B', 'C') ('B', 'D') ('C', 'C') ('C', 'D') ('D', 'D')
```

&#x20;    还有就是，combinations和permutations返回的是对象地址，原因是在python3里面，返回值已经不再是list,而是iterators（迭代器）, 所以想要使用，只用将iterator 转换成list 即可， 还有其他一些函数返回的也是一个对象，需要list转换，比如 list(map())等 。
