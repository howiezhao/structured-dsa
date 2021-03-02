# Fibonacci 查找

二分查找和 Fibonacci 查找都有一个通用策略，即对于任何的 A[0, n)，总是选取 \\(A[\lambda n]\\) 作为轴点，其中 \\(0\leq\lambda<1\\)。

具体来说，二分查找对应于 \\(\lambda=0.5\\)，Fibonacci 查找对应于 \\(\lambda=\phi=0.6180339...\\)。

比如，若设 `n=fib(k)-1`，则可取 `mi=fib(k-1)-1`，于是，前、后子向量的长度分别为 `fib(k-1)-1`、`fib(k-2)-1`。

```python
def fib_search(A, e, lo, hi):
    Fib fib(hi-lo)
    while lo < hi:
        while hi-lo<fib.get():
            fib.prev()
        mi = lo + fib.get() - 1  # 按黄金比例切分
        if e < A[mi]:
            hi = mi  # 深入前半段[lo, mi)继续查找
        elif A[mi] < e:
            lo = mi + 1  # 深入后半段(mi, hi)
        else:
            return mi  # 在mi处命中
    return -1
```

其平均时间复杂度约为 \\(O(1.44\times logn)\\)。
