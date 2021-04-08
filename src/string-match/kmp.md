# KMP

**KMP**（D.E.**K**nuth, J.H.**M**orris, V.R.**P**ratt）算法可以看作是对暴力匹配的一种改进，具体来说，在每一次失败之后，应该将模式串中的某一个字符与文本串中刚才失败的那个字符彼此重新对齐。

比如：

```python
T = 'ZHREGRETBA'
P =   'REGROW'
P =      'REGROW'
```

当 `T` 中的 `E` 与 `P` 中的 `O` 失配后，我们应将 `P` 中的 `E` 重新与 `T` 中的 `E` 进行比较，此时 `P` 向后移动了 3 位。

如何确定模式串中要进行对齐的那个继任字符呢？我们需要借助 `next` 查询表，由此可见 KMP 算法的核心在于构造 `next` 查询表。

构造查询表 `next[0, m)`：在任一位置 `P[j]` 处失败之后，将 `j` 替换为 `next[j]`。

所谓 `next[j]`，即是在 `P[0, j)` 中，最大自匹配的真前缀和真后缀的长度。

比如，`P = 'chinchilla'`：

- `next[0]`，即 `P[0, 0) == ''`：设为 -1
- `next[1]`，即 `P[0, 1) == 'c'`：真前缀为空串，真后缀也为空串，最大自匹配长度为 0
- `next[2]`，即 `P[0, 2) == 'ch'`：真前缀只有 `'c'`，真后缀只有 `'h'`，最大自匹配长度为 0
- `next[3]`，即 `P[0, 3) == 'chi'`：真前缀有 `['c', 'ch']`，真后缀有 `['i', 'hi']`，最大自匹配长度为 0
- `next[4]`，即 `P[0, 4) == 'chin'`：真前缀有 `['c', 'ch', 'chi']`，真后缀有 `['n', 'in', 'hin']`，最大自匹配长度为 0
- `next[5]`，即 `P[0, 5) == 'chinc'`：真前缀有 `['c', 'ch', 'chi', 'chin']`，真后缀有 `['c', 'nc', 'inc', 'hinc']`，最大自匹配为 `'c'`，长度为 1
- `next[6]`，即 `P[0, 6) == 'chinch'`：真前缀有 `['c', 'ch', 'chi', 'chin', 'chinc']`，真后缀有 `['h', 'ch', 'nch', 'inch', 'hinch']`，最大自匹配为 `'ch'`，长度为 2
- `next[7]`，即 `P[0, 7) == 'chinchi'`：真前缀有 `['c', 'ch', 'chi', 'chin', 'chinc', 'chinch']`，真后缀有 `['i', 'hi', 'chi', 'nchi', 'inchi', 'hinchi']`，最大自匹配为 `'chi'`，长度为 3
- `next[8]`，即 `P[0, 8) == 'chinchil'`：真前缀有 `['c', 'ch', 'chi', 'chin', 'chinc', 'chinch', 'chinchi']`，真后缀有 `['l', 'il', 'hil', 'chil', 'nchil', 'inchil', 'hinchil']`，最大自匹配长度为 0
- `next[9]`，即 `P[0, 9) == 'chinchill'`：真前缀有 `['c', 'ch', 'chi', 'chin', 'chinc', 'chinch', 'chinchi', 'chinchil']`，真后缀有 `['l', 'll', 'ill', 'hill', 'chill', 'nchill', 'inchill', 'hinchill']`，最大自匹配长度为 0

则其 `next` 表为 `[-1, 0, 0, 0, 0, 1, 2, 3, 0, 0]`。

KMP 算法实现如下：

```python
def build_next(P):  # 构造模式串P的next[]表
    m = len(P)
    j = 0  # “主”串指针
    N = [-1]  # next[]表
    t = N[0]  # 模式串指针（P[-1]通配符）
    while j < m-1:
        if t < 0 or P[j] == P[t]:  # 匹配
            j += 1
            N.append(t+1)
        else:  # 失配
            t = N[t]
    return N


def match(P, T):
    next = build_next(P)  # 构造next表
    n = len(T)
    i = 0  # 文本串指针
    m = len(P)
    j = 0  # 模式串指针
    while j < m and i < n:  # 自左向右，逐个比对字符
        if j < 0 or T[i] == P[j]:  # 若匹配
            i += 1  # 则携手共进
            j += 1
        else:  # 否则，P右移，T不回退
            j = next[j]
    del next  # 释放next表
    return i-j


# 测试
T = '1001101101'
P = '1011'
print(match(P, T))  # 4
```

在最坏情况下，其时间复杂度为 \\(O(n)\\)，具体来说，对于长度为 \\(n\\) 的文本串和长度为 \\(m\\) 的模式串，其时间复杂度为 \\(O(n+m)\\)

## 参考

- [字符串匹配的KMP算法](http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html)
- [pm_kmp.cpp](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/string_pm_kmp/pm_kmp.cpp.htm)
- [pm_kmp_next.cpp](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/string_pm_kmp/pm_kmp_next.cpp.htm)
- [pm_kmp_next_improved.cpp](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/string_pm_kmp_improved/pm_kmp_next_improved.cpp.htm)
- [pm_kmp.java](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/_java/dsa/pm_kmp.java.htm)
