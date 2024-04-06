# [Rotate Image](https://leetcode.com/problems/rotate-image/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Math`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/117acb28-2f39-4d0c-a033-aa70c03fd005)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/9bf246a5-ddb2-42cd-a408-d076770e63ec)
## Solution
```java
class Solution {
    public void rotate(int[][] matrix) {
        int row = matrix.length;
        int column = matrix[0].length;

        for (int i = 0; i < row; i++) {
            // Swap diagonally for in place transpose
            // that's why, here j = i + 1, otherwise double transpose will occur
            // Iterate over the upper triangle of the matrix
            for (int j = i + 1; j < column; j++) {
                // Swap elements across the diagonal
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        for (int j = 0; j < column / 2; j++) {
            for (int i = 0; i < row; i++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][(column - j) - 1];
                matrix[i][(column - j) - 1] = temp;
            }
        }
    }
}
```
