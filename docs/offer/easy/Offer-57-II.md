# 剑指Offer 09 和为s的连续正数序列

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

输入一个正整数```target```，输出所有和为```target```的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

 

**示例 1：**

```
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例 2：**

```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```
 

**限制：**

* 1 <= target <= 10^5

## 2. 解题思路

### 2.1 方法一：数学法

相当于等差数列前n项和求解。

```java

class Solution {
    public int[][] findContinuousSequence(int target) {
        if(target<3){
            return null;
        }
        List<int[]> vec = new ArrayList<int[]>();
        //int[][] result = new int[]();
        for(int i=(int)Math.sqrt(2*target);i>=2;i--){
            if((2*target - i*(i-1)) % (2*i) == 0){
                int[] temp = new int[i];
                for(int j = 0; j<i;j++){
                    temp[j]=(2*target - i*(i-1)) / (2*i) + j;
                }
                vec.add(temp);
            }
        }
        return vec.toArray(new int[vec.size()][]);
    }
}
```

### 2.2 方法二：双指针\滑动窗口

让两个指针一左一右前进，之和大了，左指针前进，之和小了，右指针前进。

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        int i = 1, j = 2, sum = 3;
        List<int[]> res = new ArrayList<>();

        while(i < j) {
            if(sum == target) {
                int[] arr = new int[j - i + 1];
                for(int k = i; k <= j; k++) {
                    arr[k - i] = k;
                }
                res.add(arr);
                // 滑动窗口左边界继续往右移动寻找下一个正确答案
                sum -= i;
                i++;
            } else if(sum > target) {
                sum -= i;
                i++;
            } else {
                j++;
                sum += j;
            }
        }

        return res.toArray(new int[0][]);
    }
}


```