# 插值查找

假设已知有序向量中各元素随机分布的规律，比如均匀且独立的随机分布，于是 `[lo, hi)` 内各元素应大致按照线性趋势增长，即 \\(\frac{mi-lo}{hi-lo}\approx\frac{e-A[lo]}{A[hi]-A[lo]}\\)，因此，通过猜测轴点 `mi`，可以极大地提高收敛速度，即 \\(mi\approx lo+(hi-lo)\times\frac{e-A[lo]}{A[hi]-A[lo]}\\)。

例如，在英文词典中，`binary` 大致位于 \\(\frac{2}{26}\\) 处，`search` 大致位于 \\(\frac{19}{26}\\) 处。

按照姚期智先生早期的证明，在插值查找算法中，每经过一次比较，查找规模 n 缩至 \\(\sqrt{n}\\)。

通过以上定理可以计算得出其平均时间复杂度约为 \\(O(loglogn)\\)。

在实际中，插值算法通常优势不明显 —— 除非查找区间宽度极大，或者比较操作成本极高；此外，其易受小扰动的干扰和“蒙骗”；在具体实现时须引入乘法、除法运算，这也造成其实现成本较高。

所以，实际可行的方法是：首先通过插值查找，将查找范围缩小到一定的范围，然后再进行二分查找。
