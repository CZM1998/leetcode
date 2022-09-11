# 剑指Offer 22 链表中倒数第k个节点

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有```6```个节点，从头节点开始，它们的值依次是```1、2、3、4、5、6```。这个链表的倒数第```3```个节点是值为 4 的节点。

**示例：**

```
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
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

### 2.1 方法一：双指针

在我们的题目中， 链表的长度是未知的。如果要求出倒数第k个元素，显然先求长度再用长度减去k定位目标会遍历两次链表。此时，先让一个指针前进k，再让另一个指针同时出发，先走的到了链表尾部，则后走的正好出于倒数第k个。

```java
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        if (head == null || k < 1) {
            return head;
        }
        ListNode right = head;
        ListNode left = head;
        while (k-- > 0) {
            if (right != null) {
                right = right.next;
            }
        }
        while (right != null) {
            right = right.next;
            left = left.next;
        }
        return left;
    }
}
```