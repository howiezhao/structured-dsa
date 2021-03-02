# LRU

```python
from collections import OrderedDict


class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity  # cache的容量
        self.visited = OrderedDict()  # python内置的OrderDict具备排序的功能

    def get(self, key: int) -> int:
        if key not in self.visited:
            return -1
        self.visited.move_to_end(key)  # 最近访问的放到链表最后，维护好顺序
        return self.visited[key]

    def put(self, key: int, value: int) -> None:
        if key not in self.visited and len(self.visited) == self.capacity:
            # last=False时，按照FIFO顺序弹出键值对
            # 因为我们将最近访问的放到最后，所以最远访问的就是最前的，也就是最first的，故要用FIFO顺序
            self.visited.popitem(last=False)
        self.visited[key] = value
        self.visited.move_to_end(key)    # 最近访问的放到链表最后，维护好顺序
```

LeetCode：[146. LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/)
