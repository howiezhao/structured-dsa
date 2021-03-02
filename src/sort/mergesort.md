# 归并排序

**归并排序**（merge sort）是**分治策略**的一种实现，具体来说，它将序列一分为二，分别的对子序列递归排序，最后合并有序子序列。

归并排序的核心是合并（merge）操作，即**二路归并**（2-way merge），指将两个有序序列合并为一个有序序列：`S[lo, hi) = S[lo, mi) + S[mi, hi)`。

合并时只需比较两个有序序列的第一个元素的大小即可。

```python
def merge(left, right):
    result = []
    while left and right:
        if left[0] <= right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    if left:
        result += left
    if right:
        result += right
    return result


def mergesort(lis):  # [lo, hi)
    if len(lis) < 2:  # 单元素区间自然有序，否则...
        return lis
    mi = len(lis) >> 1  # 以中点为界
    left = mergesort(lis[:mi])  # 对前半段排序
    right = mergesort(lis[mi:])  # 对后半段排序
    return merge(left, right)  # 归并


# 测试
lis = [4, 3, 8, 7, 1, 9, 6]
print(mergesort(lis))  # [1, 3, 4, 6, 7, 8, 9]
```

归并排序的最坏时间复杂度为 \\(O(nlogn)\\)。

LeetCode：[21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
