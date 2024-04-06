# [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)
## Topics: `Array`, `Binary Search`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/856de110-4399-435a-a052-40573a22816d)
## Solution
```java
import java.util.Arrays;
class Solution {
    public int search(int[] nums, int target) {
        int length = nums.length;
        int rotatedBy = 0;

        for (int i = 0; i < length - 1; i++) {
            if (nums[i + 1] < nums[i]) {
                rotatedBy = i + 1;
            }
        }
        int index = 0;
        if (rotatedBy > 0) {
            index = Arrays.binarySearch(nums, 0, rotatedBy, target);
            if (index < 0) {
                index = Arrays.binarySearch(nums, rotatedBy, length, target);
                if (index >= 0) return index;
            } else return index;
        } else {
            index = Arrays.binarySearch(nums, target);
            if (index >= 0) return index;
        }
        return -1;
    }
}
```
---
## Solution
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            }
            
            // Check if the left half is sorted
            if (nums[left] <= nums[mid]) {
                // Check if the target falls within the range [nums[left], nums[mid]]
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else { // Right half is sorted
                // Check if the target falls within the range [nums[mid], nums[right]]
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        
        return -1;
    }
}
```
