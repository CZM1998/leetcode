# 剑指Offer 32-III 从上到下打印二叉树 III

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。


例如:
给定二叉树: [3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```
 

**提示：**

1. 节点总数 <= 1000

## 2. 解题思路

### 2.1 方法一：层序遍历

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        Queue<TreeNode> help = new LinkedList<>();
        if (root != null) {
            help.add(root);
        }
        while(!help.isEmpty()) {
            LinkedList<Integer> temp = new LinkedList<>();
            int size = help.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = help.poll();
                if ((res.size() & 1) == 1) {
                    temp.addFirst(node.val);
                } else {
                    temp.addLast(node.val);
                }
                if (node.left != null) {
                    help.add(node.left);
                }
                if (node.right != null) {
                    help.add(node.right);
                }
            }
            res.add(temp);
        }
        return res;
    }
}
```