[Find Minimun in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)
## Topics: `Array`, `Binary Search`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d3acf405-819d-4fb8-b644-b1f0497f47ad)
## Solution
```java
class Solution {
    public int findMin(int[] nums) {
        int length = nums.length;
        int rotatedBy = 0;

        for (int i = 0; i < length - 1; i++) {
            if (nums[i + 1] < nums[i]) {
                rotatedBy = i + 1;
            }
        }
        return nums[rotatedBy];
    }
}
```
---
```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;

        // Perform binary search
        while (left < right) {
            int mid = left + (right - left) / 2;

            // Check if the minimum element is in the left or right half
            if (nums[mid] < nums[right]) {
                // Minimum element is in the left half
                right = mid;
            } else {
                // Minimum element is in the right half (excluding mid)
                left = mid + 1;
            }
        }

        // Left pointer points to the minimum element
        return nums[left];
    }
}
```
