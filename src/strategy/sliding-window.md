# 滑动窗口

滑动窗口一般用于解决从数组或字符串中找出**连续**的子数组或子串的问题。

给定一个数组，找出数组中连续 3 个数的最大值。如 `[1, 4, 2, 6, 4, 5, 3]` 中最大值是 15，即 `[6, 4, 5]`。

```python
nums = [1, 4, 2, 6, 4, 5, 3]


def brute(nums):
    max_value = 0
    for i in nums:
        max_value = max(max_value, sum(nums[i:i+3]))
    return max_value


def sliding_window(nums):
    start = 1
    end = 3
    max_value = sum(nums[0:2])
    while end < len(nums):
        max_value = max(max_value, max_value-nums[start-1]+nums[end])
        end += 1
        start += 1
    return max_value


brute(nums)
sliding_window(nums)
```

LeetCode：

- [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)
- [209]()
- [1456]()
