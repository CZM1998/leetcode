# 剑指Offer 07 重建二叉树

## 1. 题目概览

[点此直达题目](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
 

**示例 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```java
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**示例 2:**

```java
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```
 

限制：

`0 <= 节点个数 <= 5000`


## 2. 解题思路

### 2.1 递归

前序和中序遍历的组合可以完成对树的重建。由于二叉树遍历的性质，前序可以非常明显的确定每个子树的根节点是什么。而中序遍历能够明确的将元素划分到不同的子树中。

因此，利用前序和中序恢复二叉树的过程便是，首先利用前序确定当前子树的根节点，然后将中序划分成左右子树。通过递归的过程可以逐步划分所有的子树。

```java
class Solution {

    int[] preorder;
    HashMap<Integer, Integer> dic = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        for(int i = 0; i < inorder.length; i++)
            dic.put(inorder[i], i);
        return recur(0, 0, inorder.length - 1);
    }

    TreeNode recur(int root, int left, int right) {
        // 递归终止
        if(left > right) return null;
        // 建立根节点
        TreeNode node = new TreeNode(preorder[root]);
        // 划分根节点、左子树、右子树
        int i = dic.get(preorder[root]);                       
        // 开启左子树递归
        node.left = recur(root + 1, left, i - 1);              
        // 开启右子树递归
        node.right = recur(root + i - left + 1, i + 1, right); 
        // 回溯返回根节点
        return node;                                           
    }
}
```
