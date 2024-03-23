# [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/6940ccf7-0b1c-452d-9c68-ae0952773bf3)
## Solution
```java
import java.util.Arrays;
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix.length == 0) return false;
        if (matrix.length == 1) {
            if (matrix[0].length == 1) {
                if (matrix[0][0] == target) return true;
                return false;
            }
        }
        int l = 0;
        int u = matrix.length - 1;
        while (l <= u) {
            int index = -1;
            int mid = (l + u) / 2;
            if (target == matrix[mid][0]) return true;
            else if (target > matrix[mid][0]) {
                index = Arrays.binarySearch(matrix[mid], target);
                if (index >= 0) return true;
                l = mid + 1;
            } else if (target < matrix[mid][0]) {
                try {
                    index = Arrays.binarySearch(matrix[mid - 1], target);
                } catch (ArrayIndexOutOfBoundsException e) {
                    return false;
                }
                if (index >= 0) return true;
                u = mid - 1;
            }
        }
        return false;
    }
}
```
