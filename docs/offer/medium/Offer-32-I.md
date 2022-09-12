# 剑指Offer 32-I 从上到下打印二叉树

## 1. 题目概览

[点此直达题目](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

**例如:**

给定二叉树: `[3,9,20,null,null,15,7]`,

```java
    3
   / \
  9  20
    /  \
   15   7
```

返回：

`[3,9,20,15,7]`
 

**提示：**

1. 节点总数 <= 1000


## 2. 解题思路

### 2.1 层序遍历

利用队列分层遍历二叉树

```java
class Solution {
    public int[] levelOrder(TreeNode root) {
        if(root == null) {
            return new int[0];
        }
        Queue<TreeNode> queue = new LinkedList<>();
        List<Integer> list = new ArrayList<>();
        queue.add(root);
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            list.add(node.val);
            if(node.left != null)
                queue.add(node.left);
            if(node.right != null)
                queue.add(node.right);
        }
        int[] result = new int[list.size()];
        for(int i = 0; i < list.size(); i++) {
            result[i] = list.get(i);
        }
        return result;
    }
}
```