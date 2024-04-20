# [Find All Groups of Farmland](https://leetcode.com/problems/find-all-groups-of-farmland/description/)
## Topics: `Array`, `Depth-First Search`, `Breadth-First Search`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/a09aa904-f59d-4af5-8d28-e84817d29118)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/26aa3f8d-4a4f-422e-bbfb-94107e5214d4)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ec5da4bb-4b65-4f68-946e-b26fe0b607ea)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c527dee8-46b1-40b6-bf30-aecfcb4009d8)
## Solution
```java
class Solution {
    public int[][] findFarmland(int[][] land) {
        List<int[]> result = new ArrayList<>();
        int m = land.length;
        int n = land[0].length;
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (land[i][j] == 1) {
                    int[] topLeft = new int[]{i, j};
                    int[] bottomRight = new int[]{i, j};
                    dfs(land, i, j, topLeft, bottomRight);
                    result.add(new int[]{topLeft[0], topLeft[1], bottomRight[0], bottomRight[1]});
                }
            }
        }
        
        return result.toArray(new int[result.size()][]);
    }
    
    private void dfs(int[][] land, int i, int j, int[] topLeft, int[] bottomRight) {
        if (i < 0 || i >= land.length || j < 0 || j >= land[0].length || land[i][j] != 1) {
            return;
        }
        
        land[i][j] = 0; // Mark current cell as visited
        
        // Update top-left and bottom-right coordinates
        topLeft[0] = Math.min(topLeft[0], i);
        topLeft[1] = Math.min(topLeft[1], j);
        bottomRight[0] = Math.max(bottomRight[0], i);
        bottomRight[1] = Math.max(bottomRight[1], j);
        
        // Explore neighboring cells in all four directions
        dfs(land, i + 1, j, topLeft, bottomRight); // Down
        dfs(land, i - 1, j, topLeft, bottomRight); // Up
        dfs(land, i, j + 1, topLeft, bottomRight); // Right
        dfs(land, i, j - 1, topLeft, bottomRight); // Left
    }
}
```
