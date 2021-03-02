# KMP

构造查询表 `next[0, m)`：在任一位置 `P[j]` 处失败之后，将 `j` 替换为 `next[j]`。

所谓 `next[j]`，即是在 `P[0, j)` 中，最大自匹配的真前缀和真后缀的长度。

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
P = '1011'
T = '1001101101'
print(match(P, T))  # 4
```

在最坏情况下，其时间复杂度为 \\(O(n)\\)，具体来说，对于长度为 n 的文本串和长度为 m 的模式串，其时间复杂度为 \\(O(n+m)\\)

## 参考

- [字符串匹配的KMP算法](http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html)
- [pm_kmp.cpp](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/string_pm_kmp/pm_kmp.cpp.htm)
- [pm_kmp_next.cpp](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/string_pm_kmp/pm_kmp_next.cpp.htm)
- [pm_kmp_next_improved.cpp](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/string_pm_kmp_improved/pm_kmp_next_improved.cpp.htm)
- [pm_kmp.java](https://dsa.cs.tsinghua.edu.cn/~deng/ds/src_link/_java/dsa/pm_kmp.java.htm)
