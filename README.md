# Leetcode-Python16

## 513. Find Bottom Left Tree Value

June 06, 2023  4h

Congratulations!\
This is the sixteenth day for leetcode python study. Today we will learn more about the Binary Tree!\
The challenges today are about ~~need to delete later~~.


## 513. Find Bottom Left Tree Value
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0513.%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.md)\
[video](https://www.bilibili.com/video/BV1424y1Z7pn/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
[leetcode](https://leetcode.com/problems/find-bottom-left-tree-value/)\
找树左下角的值，本题递归偏难，反而**迭代**简单，属于模板题，两种方法掌握一下。\
此处**没有中节点的处理逻辑**，只需要先遍历左就可以。一旦得到深度最大的节点，就可以 优先遍历最左侧的节点了。\
回溯过程隐藏在的递归过程里面。
```python
# ways recursion:
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        self.max_depth = float('-inf') #全局变量 记录最大深度
        self.result = None  #全局变量 最大深度最左节点的数值
        self.traversal(root, 0)
        return self.result

    def traversal(self, node, depth):   #depth记录当前深度
        if not node.left and not node.right:    #终止条件,到达叶子结点
            if depth > self.max_depth:
                self.max_depth = depth      #更新最大深度
                self.result = node.val      #最大深度最左面的数值
        
        if node.left:       #left
            depth += 1
            self.traversal(node.left, depth)
            depth -= 1      #回溯一下
        if node.right:       #right
            depth += 1
            self.traversal(node.right, depth)
            depth -= 1      #回溯一下
```
```python
# ways 2: 迭代
from collections import deque
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0
        queue = deque()
        queue.append(root)
        while queue:
            size = len(queue)
            for i in range(size):
                node = queue.popleft()
                if i == 0:
                    result = node.val
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        return result
```



## 112
路径总和，优先掌握递归法，回溯的过程。

#### 113




## 106
从中序与后序遍历序列构造二叉树 \

#### 105.
从前序与中序遍历序列构造二叉树\
