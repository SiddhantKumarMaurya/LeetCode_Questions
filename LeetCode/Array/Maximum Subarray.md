# [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
## Topics: `Array`, `Divide and Conquer`, `Dynamic Programming`
## Problem Statemet
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/94d39fd9-c7e4-41c4-8cf0-a722d9e8d666)
## Solution (Initial Thought) (Incorrect)
```java
// This approach is ok to some extent but it missed some of the subarrays even if the array wasn't sorted
import java.util.Arrays;
class Solution {
    public int maxSubArray(int[] nums) {
        /*Arrays.sort(nums); // Sorting the won't give subarrays*/
        int maxSum = 0;
        int length = nums.length;

        for (int i = 0; i < length; i++) {
            maxSum += nums[i];
        }

        int currentSum = maxSum;
        int tempSum = maxSum;

        for (int i = 0; i < length; i++) {
            tempSum -= nums[i];
            currentSum = Math.max(tempSum, currentSum);
        }

        tempSum = maxSum;
        maxSum = Math.max(currentSum, maxSum);

        for (int i = length - 1; i >= 0; i--) {
            tempSum -= nums[i];
            maxSum = Math.max(tempSum, maxSum);
        }

        return maxSum;
    }
}
```
