# 剑指Offer 52 两个链表的第一个公共节点

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

输入两个链表，找出它们的第一个公共节点。

如下面的两个链表：

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

在节点 c1 开始相交。

**示例 1：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_1.png)


```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```


**示例 2：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_2.png)

```
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```


**示例 3：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_3.png)


```
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
```
 

**注意：**

* 如果两个链表没有交点，返回 null.
* 在返回结果后，两个链表仍须保持原有的结构。
* 可假定整个链表结构中没有循环。
* 程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。


## 2. 解题思路

### 2.1 方法一：统一长度

由于链表的性质，交叉后必然是相同的部分，那么当两个链表一样长的时候，我们就能很轻易的知道哪个结点是第一个交点。但题目中的链表长度不一定相同，所以需要先计算长度，再让指针到达同一长度的位置，此时遍历就行。

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int lengthA = length(headA);
        int lengthB = length(headB);
        ListNode max = lengthA > lengthB ? headA : headB;
        ListNode min = lengthA > lengthB ? headB : headA;
        int step = Math.abs(lengthA - lengthB);
        while(step-- > 0) {
            max = max.next;
        }
        while(max != null && min != null && max != min) {
            max = max.next;
            min = min.next;
        }
        return max;
    }

    public int length(ListNode head) {
        ListNode p = head;
        int count = 0;
        while(p != null) {
            count++;
            p = p.next;
        }
        return count;
    }
}
```

### 2.2 方法二：转换成带环的链表

对于两个链表而言，如果把另一个链表头当作自己表尾的后续，那么这个问题就从判断两个链表的交点，变成判断有环的链表的环的入口。

```
1 -> 2 -> 3 -> 4  =>  1 -> 2 -> 3 ->   4
     5 ---↑                     ↑- 5 <-|
```

但由于我们两个链表都可以进行这样的操作，因此两边同时按照环的结构前进，第一次相遇的时候就是公共交点。

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode A = headA, B = headB;
        while (A != B) {
            A = A != null ? A.next : headB;
            B = B != null ? B.next : headA;
        }
        return A;
    }
}

```