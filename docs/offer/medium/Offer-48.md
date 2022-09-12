# 剑指Offter 47 礼物的最大价值

## 1. 题目概览

[点此直达题目](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

**示例 1:**

```java
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```java
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

**提示：**

* s.length <= 40000



## 2. 解题思路

### 2.1 滑动窗口

构建一个变长的滑动窗口，让其从左至右滑动。并在滑动过程中尽可能的扩大窗口的范围。并记录窗口所能达到的最大值。

该窗口遵守以下规则：

1. 对于窗口右侧遇到的所有字符都应当包含进去。
2. 每次包含新字符后要确保窗口中没有重复字符。
3. 只能通过移动窗口左侧来去除重复字符。

对于窗口而言，其右侧的字符属于未知情况，应当全部收录。其左侧的合法最长子串的情况是已知的。即当前窗口可能不是最长的，但其左侧的情况是明确的。在遇见重复字符时，将左侧收缩到重复字符的右侧，即可保证剩余窗口中的字符均不重复。

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        // 记录重复字符去重的位置
        int[] map = new int[128];
        char[] ss = s.toCharArray();
        // 窗口左侧、右侧和最大长度
        int left = 0;
        int right = 0;
        int max = 0;
        // 避免左侧越界
        // 窗口右侧达到字符串末尾即结束
        while (left <= right && right < ss.length) {
            // 检测是否重复，并将左侧移动到去重位置
            if (map[ss[right]] > 0 && left <= map[ss[right]]) {
                left = map[ss[right]];
            }
            // 对于每个字符，应当记录下一个字符的位置
            // 因为当前重复字符必然要被抛弃
            map[ss[right]] = ++right;
            max = right - left > max ? right - left : max;
        }
        return max;
    }
}
```
