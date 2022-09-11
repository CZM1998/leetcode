# 剑指Offer 06 从尾到头打印链表

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

**示例 1：**
```
输入：head = [1,3,2]
输出：[2,3,1]
```

限制：

```0 <= 链表长度 <= 10000```

链表结构定义
```java
public class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
```

## 2. 解题思路

### 2.1 方法一：栈

我们不知道链表有多长，但只知道最先访问的元素要最后输出。那么，他必定与栈有关。而与栈有关的可以是手工栈，也可是递归。

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        LinkedList<Integer> stack = new LinkedList<Integer>();
        ListNode p = head;
        while(p != null) {
            stack.addLast(p.val);
            p = p.next;
        }
        int[] result = new int[stack.size()];
        for(int i = 0; i < result.length; i++)
            result[i] = stack.removeLast();
        return result;
    }
}
```

### 2.2 方法二：递归

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        List<Integer> temp = new ArrayList<Integer>();
        ListNode p = head;
        reverse(p, temp);
        int[] result = new int[temp.size()];
        for(int i = 0; i < result.length; i++)
            result[i] = temp.get(i);
        return result;
    }
    void reverse(ListNode p, List<Integer> temp) {
        if(p == null) return;
        reverse(p.next, temp);
        temp.add(p.val);
    }
}

```