# 剑指Offer 56-II 数组中数字出现的次数

## 1. 题目概览

[点此直达题目](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。


**示例 1：**

```java
输入：nums = [3,4,3,3]
输出：4
```

**示例 2：**

```java
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

**限制：**

* 1 <= nums.length <= 10000
* 1 <= nums[i] < 2^31

## 2. 解题思路

### 2.1 统计

只有一个数出现了一次，那么统计所有的数出现的次数就能得到唯一的那个。

```java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map  = new HashMap<Integer, Integer>();
        for(int i : nums) {
            if(!map.containsKey(i)) {
                map.put(i, 1);
            } else {
                map.put(i, map.get(i) + 1);
            }
        }
        for(Map.Entry<Integer, Integer> e : map.entrySet()) {
            if(e.getValue().equals(1)) {
                return e.getKey();
            }
        }
        return 0;
    }
}
```

### 2.2 排序后检测

排序后只需要检测当前数和后面第三个是否相同即可。

```java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map  = new HashMap<Integer, Integer>();
        for(int i : nums) {
            if(!map.containsKey(i)) {
                map.put(i, 1);
            } else {
                map.put(i, map.get(i) + 1);
            }
        }
        for(Map.Entry<Integer, Integer> e : map.entrySet()) {
            if(e.getValue().equals(1)) {
                return e.getKey();
            }
        }
        return 0;
    }
}
```

### 2.3 对应位求和取余

由于其他数均出现3次，而一个数出现一次。那么，将所有数字的二进制对应求和后取3的余，得到的就是只出现一次的数的二进制位。


```java
class Solution {
    public int singleNumber(int[] nums) {
        int count = 0;
        for(int i = 0; i < 32; i++) {
            int sub = 0;
            for(int n : nums) {
                sub += ((n >> i) & 1);
            }
            if(sub % 3 == 1) {
                count |= (1 << i);
            }
        }
        return count;
    }
}
```
