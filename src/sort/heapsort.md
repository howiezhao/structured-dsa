# 堆排序

```python
from heapq import heappush, heappop


def heapsort(iterable):
    h = []
    for value in iterable:
        heappush(h, value)
    return [heappop(h) for i in range(len(h))]


lis = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
print(heapsort(lis))
```
