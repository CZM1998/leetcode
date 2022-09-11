# 剑指Offer 09 用两个栈实现队列

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 

**示例 1：**

```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```

**示例 2：**

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

**提示：**

* 1 <= values <= 10000
* 最多会对 appendTail、deleteHead 进行 10000 次调用


## 2. 解题思路

### 2.1 方法一：双栈颠倒

s1栈负责添加元素，s2栈负责删除元素。将s1的元素放入s2，自然顺序会变成和队列一致。

```java
class CQueue {

    public Stack<Integer> s1 = new Stack<>();
    public Stack<Integer> s2 = new Stack<>();

    public CQueue() {

    }
    
    public void appendTail(int value) {
        s1.push(value);
    }
    
    public int deleteHead() {
        if (!s2.empty()) {
            return s2.pop();
        }
        if (!s1.empty()) {
            while (!s1.empty()) {
                s2.push(s1.pop());
            }
            return s2.pop();
        }
        return -1;
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```
