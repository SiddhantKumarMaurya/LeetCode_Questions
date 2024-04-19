# [Number of Islands](https://leetcode.com/problems/number-of-islands/description/)
## Topics: `Array`, `Depth-First Search`, `Breadth-First Search`, `Union Find`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/0035b8e1-213a-4db5-a7d9-f0852dc23410)
## Solution
```java
class Solution {
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        
        int m = grid.length;
        int n = grid[0].length;
        int numIslands = 0;
        
        // Iterate through each cell in the grid
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1') { // If land cell and not visited yet
                    numIslands++; // Increment island count
                    dfs(grid, i, j); // Explore neighboring land cells
                }
            }
        }
        
        return numIslands;
    }
    
    private void dfs(char[][] grid, int i, int j) {
        int m = grid.length;
        int n = grid[0].length;
        
        // Base case: Out of bounds or cell is water ('0')
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == '0') {
            return;
        }
        
        // Mark current cell as visited
        grid[i][j] = '0';
        
        // Explore neighboring cells in all four directions
        dfs(grid, i + 1, j); // Down
        dfs(grid, i - 1, j); // Up
        dfs(grid, i, j + 1); // Right
        dfs(grid, i, j - 1); // Left
    }
}
```
