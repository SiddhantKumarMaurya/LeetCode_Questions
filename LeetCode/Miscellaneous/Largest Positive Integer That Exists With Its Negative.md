# [Largest Positive Integer That Exists With Its Negative](https://leetcode.com/problems/largest-positive-integer-that-exists-with-its-negative/description/)
## Topics: `Array`, `Hash Table`, `Two Pointers`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/786041a8-af80-450c-94c7-20e51873715e)
## Solution
```java
import java.util.Arrays;
class Solution {
    public int findMaxK(int[] nums) {
        int length = nums.length;
        int left = 0;
        int right = length - 1;
        Arrays.sort(nums);

        // while (left < right && nums[left] < 0 && nums[right] > 0) will also work
        while (left < right) {
            if (nums[right] == (-nums[left])) return nums[right];
            else if (nums[right] > (-nums[left])) right--;
            else if (nums[right] < (-nums[left])) left++;
        }
        return -1;
    }
}
```
