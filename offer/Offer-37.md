# 剑指Offer 37 序列化二叉树

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

请实现两个函数，分别用来序列化和反序列化二叉树。


**示例:**

```
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```

## 2. 解题思路

### 2.1 方法一：层序遍历

对于一棵满二叉树，如果结点从上到下，从左到右，从1开始编号，那么将整棵树的结点放在数组里，有i结点，其左孩子在2i，右孩子在2i+1。

```java
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if(root == null) {
            return "[]";
        }
        // 层序遍历
        Queue<TreeNode> queue = new LinkedList<>();
        // 序列化
        StringBuilder sb = new StringBuilder();
        sb.append('[');
        // 记录连续有多少个null，用来将多余的null删除
        int count = 0;
        queue.add(root);
        // 层序遍历，并将每一层序列化
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if(node == null) {
                sb.append("null,");
                count++;
            } else {
                sb.append(String.valueOf(node.val));
                sb.append(',');
                queue.add(node.left);
                queue.add(node.right);
                // 每次遇到数字，说明还没有到最后的叶子节点
                count = 0;
            }
        }
        // 删除多的null,
        sb.delete(sb.length() - count * 5 - 1, sb.length());
        sb.append(']');
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if("[]".equals(data)) {
            return null;
        }
        // 切割方便遍历
        String[] items = data.substring(1, data.length() - 1).split(",");
        // 依然层序遍历
        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode root = new TreeNode(Integer.valueOf(items[0]));
        queue.add(root);
        // 计算当前元素该放在左子树还是右子树
        int count = 0;
        for(int i = 1; i < items.length; i++) {
            TreeNode node = null;
            if(!"null".equals(items[i])) {
                node = new TreeNode(Integer.valueOf(items[i]));
            }
            queue.add(node);
            // null没有孩子
            skipNull(queue);
            if(!queue.isEmpty()) {
                // 第二次访问时移除队列
                TreeNode parent = count % 2 == 0 ? queue.peek() : queue.poll();
                if(count % 2 == 0) {
                    parent.left = node;
                } else {
                    parent.right = node;
                }
                count++;
            }
        }
        return root;
    }

    public void skipNull(Queue<TreeNode> queue) {
        while(!queue.isEmpty()) {
            if(queue.peek() != null) {
                break;
            }
            queue.poll();
        }
    }
}
```