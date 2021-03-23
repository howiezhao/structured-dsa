# 动态规划

动态规划实际上是把原来递归的过程倒过来实现。

```python
def fib(n):
    if n < 2:
        return n
    else:
        return fib(n-1) + fib(n-2)


# Memoization 记忆化
def fib_a(n):
    M = []
    if n < 2:
        return n
    else:
        if not M[n]:
            M[n] = fib(n-1) + fib(n-2)
    return M[n]
```
