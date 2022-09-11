# 剑指Offer 28 对称的二叉树

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树```[1,2,2,3,4,4,3]```是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个```[1,2,2,null,3,null,3]```则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```
 

**示例 1：**

```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

**示例 2：**
```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

**限制：**

```
0 <= 节点个数 <= 1000
```

树结构定义
```java
public class TreeNode {
     int val;
     TreeNode left;
     TreeNode right;
     TreeNode(int x) { val = x; }
}
```

## 2. 解题思路

### 2.1 方法一：递归判断

此题值得注意的是，它的左右子树是镜像对称的，即左子树的右孩子和右子树的左孩子对应，左子树的左孩子和右子树的右孩子是对应的。因此需要按照这一规律递归判断。

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return equal(root.left, root.right);
    }

    public boolean equal(TreeNode left, TreeNode right) {
        if (left == right) {
            return true;
        }
        if (left == null || right == null || left.val != right.val) {
            return false;
        }
        return equal(left.left, right.right) && equal(left.right, right.left);
    }
}
```