# 剑指Offter 47 礼物的最大价值

## 1. 题目概览

[点此直达题目](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

**示例 1:**

```java
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```
 

**提示：**

* 0 < grid.length <= 200
* 0 < grid[0].length <= 200


## 2. 解题思路

### 2.1 动态规划

从左上角出发，只能向下和向右走。那么，对于任意一个格子，到达其的路径必然是左侧或者上方的延伸。即该格子的最大价值，取决于左侧和上方格子的最大值。

```java
class Solution {

    int[][] note = null;
    int m = 0;
    int n = 0;

    public int maxValue(int[][] grid) {
        this.m = grid.length;
        this.n = grid[0].length;
        this.note = new int[grid.length][grid[0].length];
        return maxState(grid, 0, 0);
    }

    public int maxState(int[][] grid, int x, int y) {
        if(y >= this.m || x >= this.n) {
            return 0;
        }
        if(note[y][x] > 0) {
            return note[y][x];
        }
        int max = grid[y][x];
        int state1 = maxState(grid, x + 1, y);
        int state2 = maxState(grid, x, y + 1);
        max += state1 > state2 ? state1 : state2;
        note[y][x] = max;
        return max;
    }
}
```
