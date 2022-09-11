# 剑指Offer 25 合并两个排序的链表

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

**示例1：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

**限制：**

```0 <= 链表长度 <= 1000```

## 2. 解题思路

### 2.1 方法一：头结点
由于链表有序，新建头结点，通过比较两个链表元素的大小，决定哪个元素放在头结点后。

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode temp = new ListNode();
        ListNode p = temp;
        while(l1 != null && l2 != null) {
            if(l1.val < l2.val) {
                p.next = l1;
                l1 = l1.next;
            } else {
                p.next = l2;
                l2 = l2.next;
            }
            p = p.next;
        }
        p.next = l1 != null ? l1 : l2;
        return temp.next;
    }
}
```