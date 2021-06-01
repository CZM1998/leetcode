# 剑指Offer 50 第一个只出现一次的字符

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

**示例:**

```
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
```
 

**限制：**

0 <= s 的长度 <= 50000

## 2. 解题思路

### 2.1 方法一：哈希表

```java
class Solution {
    public char firstUniqChar(String s) {
        int[] alphabet = new int[26];
        for(int i = 0; i < s.length(); i++) {
            alphabet[s.charAt(i) - 'a']++;
        }
        for(int i = 0; i < s.length(); i++) {
            if(alphabet[s.charAt(i) - 'a'] == 1) {
                return s.charAt(i);
            }
        }
        return ' ';
    }
}
```

```java
class Solution {
    public char firstUniqChar(String s) {
        if(s.length() == 0) return ' ';
        int index = s.length();
        for(char c = 'a'; c <= 'z'; c++) {
            int ci = s.indexOf(c);
            if(ci >= 0 && ci < index && ci == s.lastIndexOf(c)) {
                index = ci;
            }
        }
        return index == s.length() ? ' ' : s.charAt(index);
    }
}
```