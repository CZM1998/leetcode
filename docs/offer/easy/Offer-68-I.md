# 剑指Offer 68-I 二叉搜索树的最近公共祖先

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（**一个节点也可以是它自己的祖先**）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]


![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/binarysearchtree_improved.png)
 

**示例 1:**

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```

**示例 2:**

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
```

**说明:**

* 所有节点的值都是唯一的。
* p、q 为不同节点且均存在于给定的二叉搜索树中。

## 2. 解题思路

### 2.1 方法一：中序遍历推理

由于我们的树是一棵搜索二叉树，所以他的中序遍历是有序的。由于给出的两个结点是已知的，那么我们就能够直接知道当前结点与已知结点的位置关系。
对于公共祖先，只有三种情况：
1. p为公共祖先
2. q为公共祖先
3. 其他结点为公共祖先

由于是搜索二叉树，我们知道，其他结点必然处于p、q之间。因此，可以推论，公共祖先必须满足
$$ \min(p,q) \leq ancestor \leq max(p,q) $$

我们从根节点出发，观察三种情况。不妨设 $ p < q $
1. 情况一：p为祖先
   若p为祖先，则q必须在p的右子树中，此时p将成为我们第一个遇见满足公共祖先的要求的结点。
2. 情况二
   若q为祖先，则p必须在q的左子树中，此时q将成为我们第一个遇见满足公共祖先的要求的结点。
3. 情况三
   若p、q不为祖先，则p、q必然在某个结点的左右子树中。根据搜索二叉树的性质，我们可以推论，该结点的父节点值大于p、q值，不满足条件。该结点的子节点满足条件，但子结点的子树中必然只含有p、q中的一个。我们从root出发，该结点将成为我们第一个遇见满足公共祖先的要求的结点。

综上，我们可以推论，从root出发，第一个满足条件的结点就是公共祖先。

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode pointer = root;
        while (true) {
            // p q均在左子树
            if (pointer.val > p.val && pointer.val > q.val) {
                pointer = pointer.left;
            // p q均在右子树
            } else if (pointer.val < p.val && pointer.val < q.val) {
                pointer = pointer.right;
            } else {
                break;
            }
        }
        return pointer;
    }
}
```