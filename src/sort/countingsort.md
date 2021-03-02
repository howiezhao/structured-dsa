# 计数排序

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
