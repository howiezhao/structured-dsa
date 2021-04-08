# 暴力匹配

**暴力匹配**（Brute Force，**BF**）又称为蛮力匹配或朴素匹配算法，自左向右，以字符为单位，依次移动模式串，直到在某个位置，发现匹配。

```python
def match(P, T):
    n = len(T)  # T[i]与P[0]对齐
    m = len(P)  # T[i+j]与P[j]对齐
    for i in range(n-m+1):  # T从第i个字符起，与
        for j in range(m):  # P中对应的字符逐个比对
            if T[i+j] != P[j]:  # 若失配，P整体右移一个字符，重新比对
                break
        if j == m-1:  # 找到匹配子串
            break
    return i


# 测试
P = '1011'
T = '1001101101'
print(match(P, T))
```

暴力匹配的最坏时间复杂度为 \\(O(n\times m)\\)，\\(|\sum|\\) 越小，最坏情况出现的概率越高，\\(m\\) 越大，最坏情况的后果更加严重。
