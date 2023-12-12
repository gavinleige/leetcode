Populating Next Right Pointers in Each Node
---
### Problem
You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:



```

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}

```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.


Initially, all next pointers are set to `NULL`.


 


**Example 1:**


![](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```

**Input:** root = [1,2,3,4,5,6,7]
**Output:** [1,#,2,3,#,4,5,6,7,#]
**Explanation:** Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.

```

**Example 2:**



```

**Input:** root = []
**Output:** []

```

 


**Constraints:**


* The number of nodes in the tree is in the range `[0, 212 - 1]`.
* `-1000 <= Node.val <= 1000`


 


**Follow-up:**


* You may only use constant extra space.
* The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

### Code
[✅ Javascript](./solution.js)
### Solution
题目含义：连接二叉树的左右节点

解题思路：
- 将左子树的next指针连接到右子树
- 将右子树的next指针连接到相邻父节点的左子树
- 在前序遍历时操作

```javascript
var connect = function(root) {
    if(!root || !root.left) return root;
    root.left.next = root.right;
    root.right.next = root.next ? root.next.left : null;

    connect(root.left);
    connect(root.right);
    return root;
};
// 解法2
var connect = function(root) {
    if (root === null) return null;
    const dfs = function (n1, n2) {
      if (!n1 || !n2) return null
      n1.next = n2
      dfs(n1.left, n1.right)
      dfs(n2.left, n2.right)
      dfs(n1.right, n2.left)
    }
    dfs(root.left, root.right)
    return root
};
```

[Back to list](../README.md)