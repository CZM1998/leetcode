# 剑指Offer 58-II 左旋字符串

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

**限制：**

* ``` 1 <= k < s.length <= 10000 ```


## 2. 解题思路

### 2.1 方法一：切割后重新拼接

按照题目描述，我们将字符串分割成两部分，并将前面一部分和后面一部分交换即可。

```java
class Solution {
    public String reverseLeftWords(String s, int n){
        if(s == null || s.length() == 0 || n < 1 || n >= s.length()) {
            return s;
        }
        return s.substring(n)+s.substring(0,n);
    }
}
```

### 2.2 方法二：重新复制数组

和方法一中类似，我们新创建一个数组，将前一部分复制到后面，后一部分复制到前面，重新生成String即可。

```java
class Solution {
    public String reverseLeftWords(String s, int n){
        if(s == null || s.length() == 0 || n < 1 || n >= s.length()) {
            return s;
        }
        char[] data = s.toCharArray();
        char[] copy = new char[data.length];
        for(int i = 0; i < n; i++) {
            copy[data.length - n + i] = data[i];
        }
        for(int i = n; i < data.length; i++) {
            copy[i - n] = data[i];
        }
        return new String(copy);
    }
}
```

### 2.3 方法三：多次旋转

在上述两种方法中，都需要借助辅助空间来帮助旋转字符串。但我们可以利用多次旋转，原地获得符合题目的解。

过程：
1. 假如有一个字符串为```ab cd```且```n=2```
2. 将前后都旋转，得到```ba dc```
3. 对比期望的结果```cd ab```会发现2中的字符串与期望结果颠倒
4. 再次翻转2中字符串得到```cd ab```

```java
class Solution {
    public String reverseLeftWords(String s, int n){
        if(s == null || s.length() == 0 || n < 1 || n >= s.length()) {
            return s;
        }
        char[] data = s.toCharArray();
        reverse(data, 0, n - 1);
        reverse(data, n, data.length - 1);
        reverse(data, 0, data.length - 1);
        return new String(data);
    }

    public void reverse(char[] s, int start, int end) {
        while(start < end) {
            char temp = s[start];
            s[start] = s[end];
            s[end] = temp;
            start++;
            end--;
        }
    }
}
```