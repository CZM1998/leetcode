# 剑指Offer 57 和为s的两个数字

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

**示例 2：**

```
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```
 

**限制：**

* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^6


## 2. 解题思路

### 2.1 方法一：双指针

两个指针从两侧向中间靠近，由于数组排序，必然会存在一对数字相加为s

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left < right) {
            int sum = nums[left] + nums[right];
            if(sum == target) {
                return new int[]{nums[left], nums[right]};
            } else if(sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[0];
    }
}
```
