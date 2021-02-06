# 二叉树

节点度数不超过 2 的树称作**二叉树**（binary tree）。

二叉树是多叉树的特例，但在有根且有序时，其描述能力却足以覆盖后者。

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class BinTree:
    pass
```

## 深度优先遍历

二叉树的深度优先遍历具体分为：

- 前序遍历
- 中序遍历
- 后序遍历

前序、中序、后序是相对于根的访问顺序确定的。

### 前序遍历

前序遍历（preorder traversal）又称先序遍历，指先访问根，然后访问子树的遍历方式

```python
# 迭代实现
class Solution:
    def visit_along_left_branch(self, root: TreeNode, stack, result):
        while root:
            result.append(root.val)
            stack.append(root.right)
            root = root.left

    def preorder_traversal(self, root: TreeNode) -> List[int]:
        stack = []
        result = []
        while True:
            self.visit_along_left_branch(root, stack, result)
            if not stack:
                break
            root = stack.pop()
        return result
```

LeetCode：[144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

### 中序遍历

中序遍历（inorder traversal）指先访问左（右）子树，然后访问根，最后访问右（左）子树的遍历方式

如果二叉树画的规范的话，那么它的**垂直投影**则是中序遍历序列。

```python
# 迭代实现
class Solution:
    def go_along_left_branch(self, root: TreeNode, stack):
        while root:
            stack.append(root)
            root = root.left

    def inorder_traversal(self, root: TreeNode) -> List[int]:
        stack = []
        result = []
        while True:
            self.go_along_left_branch(root, stack)
            if not stack:
                break
            root = stack.pop()
            result.append(root.val)
            root = root.right
        return result
```

LeetCode：[94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

### 后序遍历

后序遍历（postorder traversal）指先访问子树，然后访问根的遍历方式

```python
class Solution:
    def goto_left_most_leaf(self, stack):
        while (root=stack.pop()):
            stack.append(root)
            root = root.left

    def inorder_traversal(self, root: TreeNode) -> List[int]:
        stack = []
        result = []
        if root:
            stack.append(root)
        while stack:
            if stack.top() != root.parent:
                self.go_along_left_branch(stack)
            root = stack.pop()
            result.append(root.val)
        return result
```

LeetCode：[145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

## 广度优先遍历

二叉树的广度优先遍历即层序遍历/层次遍历。

```python
from collections import deque


# 迭代实现
class Solution:
    def level_order_traversal(self, root: TreeNode) -> List[int]:
        result = []
        queue = deque()  # 引入辅助队列
        queue.append(root)  # 根节点入队
        while queue:  # 在队列再次变空之前，反复迭代
            x = queue.popleft()  # 取出队首节点，并随即
            result.append(x.val)  # 访问之
            if x.left:
                queue.append(x.left)  # 左孩子入队
            if x.right:
                queue.append(x.right)  # 右孩子入队
        return result
```

LeetCode：[102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
