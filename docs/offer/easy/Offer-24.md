# 剑指Offer 24 反转链表

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

示例:

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```
 
**限制：**

```
0 <= 节点个数 <= 5000 
```

链表结构定义
```java
public class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
```

## 2. 解题思路

### 2.1 方法一：重建链表

对于链表，我们有两种表示方式。一种是不带头结点的链表，一种是带头结点的链表。带头结点的链表，头结点不存储数据，仅用来简化操作。因此，我们可以额外新建一个头结点，同时遍历链表，将每次遍历的元素放在头结点后面，便可以完成反转。

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode list = new ListNode();
        ListNode p = head;
        ListNode temp;
        while (p != null) {
            temp = p.next;
            p.next = list.next;
            list.next = p;
            p = temp;
        }
        return list.next;
    }
}
```

### 2.2 方法二：指针反转

对于链表形式如下：
```1->2->3->4->null```

可以使用双指针方法原地反转，过程：
```
↓  ↓  ↓                ↓  ↓  ↓
   1->2->3->4->null =>  <-1  2->3->4->null
  ↓  ↓  ↓                ↓  ↓  ↓
<-1  2->3->4->null =>  <-1<-2  3->4->null
```

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode pre = null;
        ListNode cur = head;
        ListNode next = head.next;
        while (cur != null) {
            cur.next = pre;
            pre = cur;
            cur = next;
            if (next != null) {
                next = next.next;
            }
        }
        return pre;
    }
}
```

### 2.2 方法三：递归

```java
class Solution {
    ListNode last;

    public ListNode reverseList(ListNode head) {
        reverse(null, head);
        return last;
    }

    public void reverse(ListNode pre, ListNode cur) {
        if (cur == null) {
            this.last = pre;
            return;
        }
        reverse(cur, cur.next);
        cur.next = pre;
    }
}
```

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode temp = reversetList(head.next);
        head.next.next = head;
        head.next = null;
        return temp;
    }
}
```