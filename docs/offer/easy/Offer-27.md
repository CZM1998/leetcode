# 剑指Offer 27 二叉树的镜像

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

镜像输出：
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

**示例 1：**
```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

**限制：**
```0 <= 节点个数 <= 1000```

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

### 2.1 方法一：递归翻转

观察题目可知，树的每一个节点的左右子树都进行了交换。
即
```
   根节点           根节点
   /   \     ->    /    \
左子树 右子树     右子树 左子树
```
对每一棵子树，其操作均相同。

```java
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        if (root == null ) {
            return root;
        }
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        mirrorTree(root.left);
        mirrorTree(root.right);
        return root;
    }
}
```

### 2.2 方法二：层序翻转

按方法一中的图示，每一个节点均交换左右子树的位置。那么，层序遍历的时候，依然可以做到每一个节点交换左右子树。

```java
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        if (root == null) {
            return root;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            TreeNode temp = node.left;
            node.left = node.right;
            node.right = temp;
            if (node.left != null) {
                queue.add(node.left);
            }
            if (node.right != null) {
                queue.add(node.right);
            }
        }
        return root;
    }
}
```