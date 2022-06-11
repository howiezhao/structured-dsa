# 栈

栈（stack）

栈的这种特性也可以被称为**后进先出**（LIFO，Last In First Out）。

在 Python 中可以使用内置的 `list` 来实现栈的功能，如下：

```python
stack = []
stack.append(1)  # 入栈 [1]
stack.append(2)  # 入栈 [1, 2]
stack.pop()  # 出栈 [1]
stack.pop()  # 出栈 []
```

## 应用

### 括号匹配

```python
def paren(exp: str) -> bool:
    stack = []  # 使用栈记录已发现但尚未匹配的左括号
    for i in exp:  # 逐一检查当前字符
        if i is '(':  # 遇左括号：则进栈
            stack.append(i)
        elif stack:  # 遇右括号：若栈非空，则弹出左括号
            stack.pop()
        else:  # 否则（遇右括号时栈已空），必不匹配
            return False
    return False if stack else True  # 最终，栈空当且仅当匹配
```

LeetCode：[20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)
