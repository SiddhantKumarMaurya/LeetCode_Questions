# [Largest Local Values in a Matrix](https://leetcode.com/problems/largest-local-values-in-a-matrix/?envType=daily-question&envId=2024-05-12)
## Topics: `Array`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/92bf8a60-e3af-46b1-b869-534561d6662a)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/055f1301-5cf6-4524-9601-3a155d8036c3)
## Solution
```java
class Solution {
    public int[][] largestLocal(int[][] grid) {
        int n = grid.length;
        int[][] maxLocal = new int[n - 2][n - 2];

        for (int i = 1; i < n - 1; i++) {
            for (int j = 1; j < n - 1; j++) {
                int max = Integer.MIN_VALUE;
                for (int x = -1; x <= 1; x++) {
                    for (int y = -1; y <= 1; y++) {
                        max = Math.max(max, grid[i + x][j + y]);
                    }
                }
                maxLocal[i - 1][j - 1] = max;
            }
        }

        return maxLocal;
    }
}
```
