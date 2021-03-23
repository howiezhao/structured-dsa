# 刷题总结

## 套路

题目中有 *最大* 或 *最小* 的，一般都可以先通过排序再解决。

## Python

`max` 函数获取一个列表的最大值：

```python
a = [1, 0, 3]
print(max(a))  # 3
```

`bin` 函数用于生成一个数值的二进制形式：

```python
a = 55
bin(a)  # '0b110111'
```

统计序列中某元素出现的次数：

```python
a = [1, 0, 0]
a.count(0)  # 2
```

集合的交集、并集、差集：

```python
a = {1, 2, 3}
b = {1, 2, 3, 4, 5}
a & b  # 交集，输出 {1, 2, 3}
a | b  # 并集，输出 {1, 2, 3, 4, 5}
b - a  # 差集，输出 {4, 5}
```

`collections` 模块里的 `Counter` 对象可以很方便的统计元素出现的次数，如下：

```python
from collections import Counter
dict(Counter('gallahad'))  # {'g': 1, 'a': 3, 'l': 2, 'h': 1, 'd': 1}
dict(Counter('gallahad').most_common())  # {'a': 3, 'l': 2, 'g': 1, 'h': 1, 'd': 1}
```

`itertools` 模块里提供有排列组合的相关函数，如下：

```python
from itertools import permutations, combinations
nums = [1, 2, 3]
# 排列，输出 [(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)]
list(permutations(nums, 3))
# 组合，输出 [(1, 2), (1, 3), (2, 3)]
list(combinations(nums, 2))
```
