# 链表

**链表**（linked list）又称为列表（list）。

链表即物理空间不连续的线性序列，其中的元素称作**节点**（node），各节点通过指针或引用彼此连接，在**逻辑**上构成一个线性序列。

相邻节点彼此互称**前驱**（predecessor）或**后继**（successor），前驱或后继若存在，则必然唯一，没有前驱的唯一节点称作**首**（first/front）节点，没有后继的唯一节点称作**末**（last/rear）节点。

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


class List:
    pass
```

## 查找

## 增加

## 删除

LeetCode：[206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)
