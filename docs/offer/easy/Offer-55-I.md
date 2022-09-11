# 剑指Offer 55-I 二叉树的深度

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

例如：

给定二叉树 ```[3,9,20,null,null,15,7]```，
```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度 3 。

**提示：**
1. ```节点总数 <= 10000```

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

### 2.1 方法一：递归累加

对于树这种在结构上局部与整体相似，概念也是自我递归的数据结构，自然而然的会考虑使用递归求解。
因此题目可以描述成：```树的深度 = max(左子树深度,右子树深度) + 1```.
而左右子树的深度求法和上述一致，递归求解。

```java
class Solution {
    public int maxDepth(TreeNode root) {
        return depth(root);
    }

    public int depth(TreeNode root) {
        if(root == null) {
            return 0;
        }
        int left = depth(root.left);
        int right = depth(root.right);
        return left > right ? left + 1 : right + 1;
    }
}
```

### 2.2 方法二：统计层数

在树中，深度与层数是对应的，有多少层，树就有多深。因此，通过层序遍历可以得到深度。

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        List<TreeNode> queue = new LinkedList<>();
        List<TreeNode> nextLayer;
        queue.add(root);
        int depth = 0;
        while (!queue.isEmpty()) {
            nextLayer = new LinkedList<>();
            for(TreeNode node : queue) {
                if (node.left != null) {
                    nextLayer.add(node.left);
                }
                if (node.right != null) {
                    nextLayer.add(node.right);
                }
            }
            queue = nextLayer;
            depth++;
        }
        return depth;
    }
}
```