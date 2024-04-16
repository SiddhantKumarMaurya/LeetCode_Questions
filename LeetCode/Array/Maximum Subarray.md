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
---
## Solution (Kadane's Algorithm)
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0];
        int currentSum = nums[0];

        for (int i = 1; i < nums.length; i++) {
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }
}
```
---
## Solution (Divide and Conquer)
```java
class Solution {
    public int maxSubArray(int[] nums) {
        return maxSubArray(nums, 0, nums.length - 1);
    }

    private int maxSubArray(int[] nums, int left, int right) {
        if (left == right) {
            return nums[left]; // Base case: single element
        }

        int mid = left + (right - left) / 2;
        
        // Find the maximum subarray sum in the left and right halves recursively
        int maxLeftSum = maxSubArray(nums, left, mid);
        int maxRightSum = maxSubArray(nums, mid + 1, right);

        // Find the maximum subarray sum crossing the midpoint
        int maxCrossingSum = maxCrossingSum(nums, left, mid, right);

        // Return the maximum of the three sums
        return Math.max(Math.max(maxLeftSum, maxRightSum), maxCrossingSum);
    }

    private int maxCrossingSum(int[] nums, int left, int mid, int right) {
        int leftSum = Integer.MIN_VALUE;
        int sum = 0;
        for (int i = mid; i >= left; i--) {
            sum += nums[i];
            leftSum = Math.max(leftSum, sum);
        }

        int rightSum = Integer.MIN_VALUE;
        sum = 0;
        for (int i = mid + 1; i <= right; i++) {
            sum += nums[i];
            rightSum = Math.max(rightSum, sum);
        }

        return leftSum + rightSum;
    }
}
```
