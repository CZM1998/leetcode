# 剑指Offter 04 二维数组中的查找

## 1. 题目概览

[点此直达题目](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。


**示例:**


现有矩阵 matrix 如下：
```python
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = 5，返回 true。

给定 target = 20，返回 false。

 

**限制：**

`0 <= n <= 1000`

`0 <= m <= 1000`


## 2. 解题思路

### 2.1 倒序查找

由于该数组中的元素是从左到右逐渐增大，并且是从上到下逐渐增大。那么，对于某个元素，其左侧均小于它，下方均大于大。即可以按照它与目标值的大小进行移动。

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if (matrix.length == 0) {
            return false;
        }
        int n = 0;
        int m = matrix[0].length - 1;
        while (n < matrix.length && m >= 0) {
            if (target == matrix[n][m]) {
                return true;
            } else if (target < matrix[n][m]) {
                m--;
            } else {
                n++;
            }
        }
        return false;
    }
}
```
