# [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/219f212f-8edf-46c8-b3ac-f83c6b599fef)
## Solution
`Time Complexity: O(n)`
```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int length = nums.length;
        int windowStart = 0;
        int currentSum = 0;
        int minWindowSize = Integer.MAX_VALUE;

        for (int windowEnd = 0; windowEnd < length; windowEnd++) {
            currentSum += nums[windowEnd];
            while (currentSum >= target) {
                minWindowSize = Math.min(minWindowSize, windowEnd - windowStart + 1);
                currentSum -= nums[windowStart++];
            }
        }
        return (minWindowSize == Integer.MAX_VALUE) ? 0 : minWindowSize;
    }
}
```
