# 排序

排序是指：给定 n 个整数，将它们按（非降）序排列。

排序算法大致可分为两类：

- 基于比较的排序：冒泡排序、归并排序、快速排序、希尔排序，其时间复杂度的下限为 \\(O(nlogn)\\)
- 非基于比较的排序：桶排序、计数排序、基数排序

## 冒泡排序

冒泡排序（bubble sort）又称起泡排序。它主要基于以下观察：

- **有序**序列中，**任意**一对相邻元素**顺序**
- **无序**序列中，**总有**一对相邻元素**逆序**

为此，要执行扫描交换，即依次比较每一对相邻元素，如有必要，交换之；若整趟扫描都没有进行交换，则排序完成；否则，再做一趟扫描交换。

```c
void bubblesort(int A[], int n)
{
    for(bool sorted = false; sorted = !sorted; n--)  // 逐趟扫描交换，直至完全有序
    {
        for(int i = 1; i < n; i++)  // 自左向右，逐对检查A[0, n)内各相邻元素
        {
            if(A[i-1] > A[i])  // 若逆序，则
            {
                swap(A[i-1], A[i]);  // 令其互换，同时
                sorted = false;  // 清除（全局）有序标志
            }
        }
    }
}
```

## 计数排序

```python
def countingsort(lis):
    length = max(lis)-min(lis)+1
    count = [0]*length
    for i in lis:
        count[i] += 1
    for index in range(0, len(count)):
        count[index] += count[index-1]
    return count


lis = [6, 3, 8, 4, 2, 6, 3, 7, 3]
sorted_list = countingsort(lis)
print(sorted_list)
```

LeetCode：[1122. 数组的相对排序](https://leetcode-cn.com/problems/relative-sort-array/)

## 桶排序

LeetCode：[164. 最大间距](https://leetcode-cn.com/problems/maximum-gap/)
