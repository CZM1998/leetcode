# 剑指Offer 35 复杂链表的复制

## 1. 题目概览

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

**示例 1：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e1.png)

```java
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
示例 2：
```

**示例 2：**
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e2.png)

```java
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
示例 3：
```

**示例 3：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e3.png)

```java
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
示例 4：
```

```java
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。
```

**提示：**


* -10000 <= Node.val <= 10000
* Node.random 为空（null）或指向链表中的节点。
* 节点数目不超过 1000 。


## 2. 解题思路

### 2.1 哈希表辅助

相较于普通的链表，复杂链表多了一个随机的指针。这就意味着，在复制链表的过程中，某些随机指针指向的结点还没有被复制出来。因此，在第一次遍历的时候复制结点，并建立原始结点和复制结点的对应关系。第二次遍历的时候，将之前的随机指针修改为对应的节点。

```java
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) {
            return null;
        }
        Map<Node, Node> map = new HashMap<Node, Node>();
        Node temp = new Node(0);
        Node p = head;
        Node q = temp;
        while(p != null) {
            Node node = new Node(p.val);
            q.next = node;
            q = q.next;
            map.put(p, node);
            p = p.next;
        }
        p = head;
        q = temp.next;
        while(p != null) {
            Node node = map.get(p.random);
            q.random = node;
            p = p.next;
            q = q.next;
        }
        return temp.next;
    }
}
```

### 2.2 借助原链表关系

除了借助哈希表记录原结点和复制结点的关系之外，我们还可以借助链表自身的结构来记录原结点和复制结点的关系。即将复制结点直接拼接在原结点后面。

这让原始链表变成 原结点->复制结点->原结点 这样的结果。每一个原结点后面必然接一个复制结点。那么在遍历的过程中，我们就能很轻易的将复制结点的随机指针连接上。

```java
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;
        Node cur = head;
        // 1. 复制各节点，并构建拼接链表
        while(cur != null) {
            Node tmp = new Node(cur.val);
            tmp.next = cur.next;
            cur.next = tmp;
            cur = tmp.next;
        }
        // 2. 构建各新节点的 random 指向
        cur = head;
        while(cur != null) {
            if(cur.random != null)
                cur.next.random = cur.random.next;
            cur = cur.next.next;
        }
        // 3. 拆分两链表
        cur = head.next;
        Node pre = head, res = head.next;
        while(cur.next != null) {
            pre.next = pre.next.next;
            cur.next = cur.next.next;
            pre = pre.next;
            cur = cur.next;
        }
        pre.next = null; // 单独处理原链表尾节点
        return res;      // 返回新链表头节点
    }
}
```
