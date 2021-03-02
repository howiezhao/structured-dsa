# 队列

队列（queue）

在 Python 中可以使用内置的 collections.deque 来实现队列的功能，如下：

```python
from collections import deque

queue = deque()
queue.append(1)  # 入队
queue.append(2)  # 入队
queue.popleft()  # 出队
queue.popleft()  # 出队
```
