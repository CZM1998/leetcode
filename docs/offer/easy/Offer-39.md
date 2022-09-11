# 剑指Offer 39 数组中出现次数超过一半的数字

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

 

你可以假设数组是非空的，并且给定的数组总是存在多数元素。
 

**示例 1:**

```
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```
 

**限制：**

1. <= 数组长度 <= 50000

## 2. 解题思路

### 2.1 方法一：排序


由于众数数量必然超过一半，所以排序后取中间位置即可

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}
```

### 2.2 方法二：统计法

由于众数是最多的数，可以使用哈希表进行统计

```java
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> counts = new HashMap<>();
        int length = nums.length;
        for (int i = 0; i < length; i++) {
            int count = counts.getOrDefault(nums[i], 0) + 1;
            //如果某个数字出现的个数已经超过数组的一半，自己返回
            if (count > length / 2)
                return nums[i];
            counts.put(nums[i], count);
        }
        return -1;
    }
}
```

### 2.3 方法三：摩尔投票（一换一）

摩尔投票是此题的最佳解法，理解摩尔投票用一个词语就行，即：一换一。
由于题目中的众数必然是超过一半的数字，那么众数和非众数一换一，最后剩下的数字肯定是众数。
因此，题目的操作便可以变成：
1. 两数不同，抵消
2. 两数相同，保留

```java
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        int select = 0;
        for(int i = 0; i < nums.length; i++) {
            if(count == 0) {
                select = nums[i];
            }
            if(nums[i] == select) {
                count++;
            } else {
                count--;
            }
        }
        return select;
    }
}
```
