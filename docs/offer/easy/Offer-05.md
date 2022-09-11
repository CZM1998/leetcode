# 剑指Offer 05 替换空格

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/submissions/)

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

**示例 1：**
```
输入：s = "We are happy."
输出："We%20are%20happy."
```
 

限制：

```0 <= s 的长度 <= 10000```

## 2. 解题思路

### 2.1 方法一：使用辅助空间

```java
class Solution {
    public String replaceSpace(String s) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            sb.append(s.charAt(i) == ' ' ? "%20" : s.charAt(i));
        }
        return sb.toString();
    }
}
```

你还可以直接使用replace