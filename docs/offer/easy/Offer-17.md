# 剑指Offer 17 打印从1到最大的n位数

## 1. 题目概览

[点此直达题目](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

输入数字```n```，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

**示例 1:**

```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```
 

说明：

* 用返回一个整数列表来代替打印
* n 为正整数

## 2. 解题思路

### 2.1 方法一：确定上界

按题意，我们要生成$ [i, 10^n-1] $ 范围的数字，但根据评论区，此题在原书上需要考虑大数问题，而题目给定的范围却在int，所以给出两种解法。

普通的解法
```java
class Solution {
    public int[] printNumbers(int n) {
        int length = (int) Math.pow(10, n) - 1;
        int[] result = new int[length];
        for(int i = 0; i < length; i++) {
            result[i] = i + 1;
        }
        return result;
    }
}
```

考虑大数并转化成int
```java
class Solution {

    List<String> result = new LinkedList<>();
    char[] number = {'0','1','2','3','4','5','6','7','8','9'};
    int n = 0;
    
    public int[] printNumbers(int n) {
        this.n = n;
        build(new StringBuilder(), 0);
        int[] digits = new int[result.size() - 1];
        int index = 0;
        for (String item : result) {
            int num = Integer.parseInt(item);
            if (num != 0) {
                digits[index++] = num;
            }
        }
        return digits;
    }

    public void build(StringBuilder sb, int index) {
        for (char item : number) {
            sb.insert(index, item);
            if (index + 1 == this.n) {
                this.result.add(sb.toString());
            } else {
                build(sb, index + 1);
            }
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```