# 二分查找

二分查找是减治策略的一种体现。

以任一元素 `x = S[mi]` 为界，都可将待查找区间分为 2 部分，即 `S[lo, mi) <= S[mi, hi)`，其中 `S[mi]` 称作轴点，只需将目标元素 `e` 与 `x` 做一比较，即可分 2 种情况进一步处理：

1. `e < x`：则 e 若存在必属于**左**侧子区间 `S[lo, mi)`，故可递归深入
2. `x <= e`：则 e 若存在必属于**右**侧子区间 `S[mi, hi)`，亦可递归深入

二分（折半）策略：轴点 mi 总是取作中点，则查找每深入一层，问题规模也缩减**一半**。

此外，为了语义约定，查找的返回值为不大于 e 的最后一个元素。

```python
def bin_search(A, e, lo, hi):  # 在有序向量区间[lo, hi)内查找元素e
    while lo < hi:  # 不变性：A[0, lo) <= e < A[hi, n)
        mi = (lo+hi) >> 1  # 以中点为轴点，经比较后确定深入
        if e < A[mi]:
            hi = mi  # 深入前半段[lo, mi)继续查找
        else:
            lo = mi + 1  # 深入后半段(mi, hi)
    return lo-1  # 出口时，A[lo=hi]为大于e的最小元素，故lo-1即不大于e的元素的最大秩


# 测试
lis = [2, 5, 6, 9, 10, 12, 13]
print(bin_search(lis, 12, 0, len(lis)))  # 5
print(bin_search(lis, 11, 0, len(lis)))  # 4
```

其平均时间复杂度约为 \\(O(1.5\times logn)\\)。

LeetCode：[704. 二分查找](https://leetcode-cn.com/problems/binary-search/)
