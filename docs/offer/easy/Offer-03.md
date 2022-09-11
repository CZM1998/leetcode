# 剑指Offer 03 数组中重复的数字

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```
 

**限制：**

* 2 <= n <= 100000

## 2. 解题思路

### 2.1 方法一：哈希表

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> dic = new HashSet<>();
        for(int num : nums) {
            if(dic.contains(num)) return num;
            dic.add(num);
        }
        return -1;
    }
}
```

### 2.2 方法二：仿照哈希

使用哈希表时，我们是将元素映射到某个位置，第二次再次映射到这个位置的时候，就知道元素重复。但我们注意到题目说元素在0~n-1的范围内，也就是每个元素都和数组本身的某个位置对应。那么，我们可以直接把元素当作下标，去查看对应位置的元素与自己是不是相同的，若不相同，交换位置，相同则重复。相当于利用数组本身作为哈希表。

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        for(int i = 0; i < nums.length; i++) {
            int index = nums[i];
            // 避免自身和自身对比
            if(index != i && nums[index] == index) {
                return index;
            } else {
                nums[i] = nums[index];
                nums[index] = index;
            }
        }
        return -1;
    }
}
```