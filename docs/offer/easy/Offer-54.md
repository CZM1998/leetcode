# 剑指Offer 54 二叉搜索树的第k大节点

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

给定一棵二叉搜索树，请找出其中第k大的节点。

```
示例 1:

输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

示例 2:
```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```
 

**限制：**

1 ≤ k ≤ 二叉搜索树元素个数

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

对于一棵二叉搜索树，我们知道它的中序遍历的序列便是从小到大的一个非递减序列。所以将中序遍历的步骤左右颠倒一下，便可以得到从大到小的非递增序列。此时取第K个即可。

```java
class Solution {
    int max;
    int k;
    boolean findMax = false;
    
    public int kthLargest(TreeNode root, int k) {
        this.k = k;
        find(root);
        return this.max;
    }

    public void find(TreeNode root){
        if(this.findMax || root == null){
            return;
        }
        find(root.right);
        if(--this.k == 0){
            findMax = true;
            this.max = root.val;
            return;
        }
        find(root.left);
    }
}
```