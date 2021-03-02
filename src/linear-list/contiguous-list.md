# 顺序表

**顺序表**（contiguous list）又称为向量（vector）或数组（array）。

顺序表即物理空间连续的序列，A[i] 的物理地址 = A + i*s，s 为单个元素占用的空间量。

顺序表可分为**无序顺序表**和**有序顺序表**。

## 扩容

相比递增式扩容，采用加倍式扩容，每次扩容的分摊成本仅为 \\(O(1)\\)，而递增式扩容每次扩容的分摊成本则为 \\(O(n)\\)。

## 无序顺序表

无序顺序表要求元素之间至少应该能比较是否相等，我们称作**比对**操作。

### 无序顺序表的去重

Python 实现：

```python
def deduplicate(lis):  # 删除重复元素，返回被删除元素数目
    old_size = len(lis)  # 记录原规模
    i = 1  # 从lis[1]开始
    while i < len(lis):  # 自前向后逐一考察各元素lis[i]
        try:
            lis[:i].index(lis[i])  # 在前缀中寻找雷同者
            lis.pop(i)  # 若有雷同则删除雷同者（至多一个？！）
        except ValueError:
            i += 1  # 否则继续考察其后继
    return old_size-len(lis)  # 顺序表规模变化量，即删除元素总数


# 测试
lis = [3, 3, 3, 1, 9, 8, 7, 2, 1, 2]
print(deduplicate(lis))  # 4
```

对于规模为 n 的顺序表，其最坏时间复杂度为 \\(O(n^2)\\)。

## 有序顺序表

有序顺序表要求能够判定任何一对元素孰大孰小，我们称作**比较**操作。

无序顺序表经预处理转换为有序顺序表之后，相关算法多可优化。

### 有序性

*有序* 序列中，*任意* 一对相邻元素 *顺序*；*无序* 序列中，*总有* 一对相邻元素 *逆序*。因此，相邻逆序对的数目，可用以度量顺序表的逆序程度。

注意：**相邻逆序对**即两个相邻的元素 `{..i, j..}` 且 `i>j`。而**逆序数**是逆序对的个数，并不要求二者相邻。

```python
def disordered(lis):  # 返回逆序相邻元素对的总数
    n = 0  # 计数器
    for i in range(1, len(lis)):  # 逐一检查各对相邻元素
        n += (lis[i-1] > lis[i])  # 逆序则计数
    return n  # 向量有序当且仅当n=0


# 测试
lis = [3, 3, 3, 1, 9, 8, 7, 2, 1, 2]
print(disordered(lis))  # 5
```

若只需判断是否有序，则首次遇到逆序对之后，即可立即终止。

### 有序顺序表的去重

在有序顺序表中，重复的元素必然相互紧邻构成一个区间，因此，每一区间只需保留单个元素即可。

Python 实现：

```python
def uniquify(lis):
    i = 0
    j = 1  # 各对互异“相邻”元素的秩
    while j < len(lis):  # 逐一扫描，直至末元素
        if lis[i] != lis[j]:  # 跳过雷同者；发现不同元素时，向前移至紧邻于前者右侧
            i += 1
            lis[i] = lis[j]
        j += 1
    i += 1  # 直接截除尾部多余元素
    return j-i  # 顺序表规模变化量，即被删除元素总数


# 测试
lis = [1, 1, 2, 2, 3, 3, 3, 7, 8, 9]
print(uniquify(lis))  # 4
```

C 语言实现：

```c
int removeDuplicates(int* nums, int numsSize)
{
    if(numsSize == 0)
    {
        return 0;
    }
    int i = 0, j = 0;
    while(++j < numsSize)
    {
        if(nums[i] != nums[j])
        {
            nums[++i] = nums[j];
        }
    }
    return ++i
}
```

对于规模为 n 的顺序表，其最坏时间复杂度为 \\(O(n)\\)。

LeetCode：[26. 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

## 语言实现

在 Python 中可以使用内置的 list 来实现顺序表的功能，如下：

```python
contiguous_list = []
# 增加
contiguous_list.insert(0, 5)
contiguous_list.insert(0, 6)
contiguous_list.insert(2, 9)
contiguous_list.insert(3, 5)
# 删除
contiguous_list.pop(1)
# 查找
contiguous_list[0]
# 去重
contiguous_list = list(set(contiguous_list))
# 反转
contiguous_list.reverse()
```
