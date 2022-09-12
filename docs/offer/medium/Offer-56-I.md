# 剑指Offer 56-I 数组中数字出现的次数

## 1. 题目概览

[点此直达题目](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

**示例 1：**

```java
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
```

**示例 2：**

```java
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]
```
 

**限制：**

1. 2 <= nums.length <= 10000
 
## 2. 解题思路

### 2.1 分组异或

两个相同的数异或后就会消失。一个不同的数和两个相同的数异或后，会剩下不同的数。如果题目中只有一个不同的数，那么将所有数异或后即可获得那个不同的数。但两个不同的数就只会剩下两个不同数的异或值。

但如果我们可以将两个数分到两个组中，即可将问题转化成只有一个不同数的问题。在异或中，两个不同的值为真。因此，我们可以按照异或后，二进制中某一位是否为1来分组。即完成对不同数的分组。

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        int ret = 0;
        for (int n : nums) {
            ret ^= n;
        }
        int div = 1;
        while ((div & ret) == 0) {
            div <<= 1;
        }
        int a = 0, b = 0;
        for (int n : nums) {
            if ((div & n) != 0) {
                a ^= n;
            } else {
                b ^= n;
            }
        }
        return new int[]{a, b};
    }
}
```