# [Score After Flipping Matrix](https://leetcode.com/problems/score-after-flipping-matrix/description/?envType=daily-question&envId=2024-05-13)
## Topics: `Array`, `Greedy`, `Bit Manipulation`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/74464323-f076-4fc2-aa27-e92a5c229b68)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/207720fd-c274-4795-a058-0bbf9ef88008)
## Solution
```java
class Solution {
    public int matrixScore(int[][] grid) {
        int n = grid.length;
        int m = grid[0].length;
        int res = (1 << (m - 1)) * n;

        for (int j = 1; j < m; ++j) {
            int val = 1 << (m - 1 - j);
            int set = 0;

            for (int i = 0; i < n; ++i) {
                if (grid[i][j] == grid[i][0]) {
                    set++;
                }
            }

            res += Math.max(set, n - set) * val;
        }

        return res;
    }
}
```
