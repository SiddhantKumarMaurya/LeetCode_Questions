# [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/description/)
## Topics: `Array`, `Dynamic Programming`, `Stack`, `Matrix`, `Monotonic Stack`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/eba59406-182d-4e1c-9ca8-6538f35fbf6b)
## Solution
`Approach used: Dynamic Programming along with largest rectangle in histogram`
```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        
        int rows = matrix.length;
        int cols = matrix[0].length;
        int maxArea = 0;
        int[] heights = new int[cols];
        
        for (int i = 0; i < rows; i++) {
            // Update heights array based on the current row
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j] == '1') {
                    heights[j]++;
                } else {
                    heights[j] = 0;
                }
            }
            
            // Calculate the largest rectangle area using heights array
            maxArea = Math.max(maxArea, largestRectangleArea(heights));
        }
        
        return maxArea;
    }
    
    private int largestRectangleArea(int[] heights) {
        int maxArea = 0;
        int n = heights.length;
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 0; i <= n; i++) {
            while (!stack.isEmpty() && (i == n || heights[i] < heights[stack.peek()])) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }
            stack.push(i);
        }
        
        return maxArea;
    }
}
```
