# [Special Array With X Elements Greater Than or Equal X](https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x/description/)
## Topics: `Array`, `Binary Search`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/aa46e214-8847-4f90-82f4-f8edd62f6b45)
## Solution (Slow: Takes 2ms and beats only 47.70% of users with Java)
```java
import java.util.Arrays;
class Solution {
    public int specialArray(int[] nums) {
        int length = nums.length;
        Arrays.sort(nums);
        int left = 0;
        int right = length - 1;
        int x = -1;
        for (int i = 0; i <= length; i++) {
            if (getRange(nums, i) == i) {
                x = i;
            }
        }
        return x;
    }

    public int getRange(int[] nums, int target) {
        int length = nums.length;
        for (int i = 0; i < length; i++) {
            if (nums[i] >= target) {
                return length - i;
            } 
        }
        return -1;
    }
}
```
---
## Solution (Slow)
```java
import java.util.Arrays;

class Solution {
    public int specialArray(int[] nums) {
        Arrays.sort(nums);  // Sort the array
        int n = nums.length;

        // Iterate through possible values of x from 1 to n
        for (int x = 1; x <= n; x++) {
            // Find the number of elements greater than or equal to x using binary search
            int count = countGreaterOrEqual(nums, x);
            if (count == x) {
                return x;
            }
        }

        return -1;  // If no such x is found
    }

    private int countGreaterOrEqual(int[] nums, int x) {
        int left = 0, right = nums.length;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= x) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return nums.length - left;  // Count of elements >= x
    }
}
```
## Solution (Takes 0ms)
```java
class Solution {
    public int specialArray(int[] nums) {
        int[] numCounts = new int[nums.length+1];
        for(int num: nums)
            if(num>nums.length)
                numCounts[nums.length]++;
            else
                numCounts[num]++;
        int bigNumsCount = 0;
        for(int specialGuess = nums.length; specialGuess>0; specialGuess--){
            bigNumsCount += numCounts[specialGuess];
            if(bigNumsCount > specialGuess)
                return -1;
            if(bigNumsCount == specialGuess)
                return specialGuess;
        }
        return -1;
    }
}
```
