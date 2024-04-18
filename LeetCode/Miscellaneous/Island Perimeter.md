# [Island Perimeter](https://leetcode.com/problems/island-perimeter/description/)
## Topics: `Array`, `Depth-First Search`, `Breadth-First Serach`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/98eedc3b-410f-4c9c-910a-0f3b7ab197f8)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/20749453-322a-43cd-8ebd-98610b9da053)
## Solution
```java
class Solution {
    public int islandPerimeter(int[][] grid) {
        int perimeter = 0;
        int rows = grid.length;
        int cols = grid[0].length;
        
        // Iterate through each cell in the grid
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                // Check if the current cell is land
                if (grid[i][j] == 1) {
                    // Check its adjacent cells
                    perimeter += 4; // Initialize perimeter to 4 for each land cell
                    
                    // Check up
                    if (i > 0 && grid[i - 1][j] == 1) {
                        perimeter--;
                    }
                    // Check down
                    if (i < rows - 1 && grid[i + 1][j] == 1) {
                        perimeter--;
                    }
                    // Check left
                    if (j > 0 && grid[i][j - 1] == 1) {
                        perimeter--;
                    }
                    // Check right
                    if (j < cols - 1 && grid[i][j + 1] == 1) {
                        perimeter--;
                    }
                }
            }
        }
        
        return perimeter;
    }
}

```
