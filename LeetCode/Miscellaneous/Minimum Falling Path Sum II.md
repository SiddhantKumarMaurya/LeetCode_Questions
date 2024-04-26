# [Minimum Falling Path Sum II](https://leetcode.com/problems/minimum-falling-path-sum-ii/description/)
## Topics: `Array`, `Dynamic Programming`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/48de9303-3fe0-4106-9837-dc775a5e33cc)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/81aeb7a1-049c-4de2-9155-9c3bdece408f)
## Solution:
```java
public class Solution {
    public int minFallingPathSum(int[][] grid) {
        int n = grid.length;
        int[][] dp = new int[n][n];
        
        // Initialize the first row of dp with the values of the first row of the grid
        for (int i = 0; i < n; i++) {
            dp[0][i] = grid[0][i];
        }
        
        // Iterate from the second row onwards
        for (int i = 1; i < n; i++) {
            // Iterate through each cell in the current row
            for (int j = 0; j < n; j++) {
                // Find the minimum falling path sum from the previous row, excluding the element in the same column
                int minPrev = Integer.MAX_VALUE;
                for (int k = 0; k < n; k++) {
                    if (k != j) {
                        minPrev = Math.min(minPrev, dp[i - 1][k]);
                    }
                }
                // Update the current cell with the sum of its value and the minimum falling path sum found
                dp[i][j] = grid[i][j] + minPrev;
            }
        }
        
        // Find the minimum falling path sum in the last row
        int minSum = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            minSum = Math.min(minSum, dp[n - 1][i]);
        }
        
        return minSum;
    }
}
```
