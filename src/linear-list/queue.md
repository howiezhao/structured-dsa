# 队列

**队列**（queue）也是**受限**的序列，其只能在队尾插入（enqueue），只能在队头删除（dequeue）。

队列的这种特性也可以被称为**先进先出**（FIFO，First In First Out）。

队列可以基于顺序表或链表实现。

在 Python 中可以使用内置的 `collections.deque` 来实现队列的功能，如下：

```python
from collections import deque

queue = deque()
queue.append(1)  # 入队 [1]
queue.append(2)  # 入队 [1, 2]
queue.popleft()  # 出队 [2]
queue.popleft()  # 出队 []
```

LeetCode：[剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)
