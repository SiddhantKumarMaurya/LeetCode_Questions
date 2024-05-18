## [Jump Game II](https://leetcode.com/problems/jump-game-ii/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Dynamic Programming`, `Greedy`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/93d7cf68-c3ba-43b9-9562-5636e28bc35e)
## Solution (Greedy Approach)
```java
class Solution {
    public int jump(int[] nums) {
        if (nums.length == 1) return 0; // No jumps needed if there's only one element

        int jumps = 0; // Number of jumps made
        int currentEnd = 0; // End of the range that can be reached with the current number of jumps
        int furthest = 0; // Furthest point that can be reached with the next jump

        for (int i = 0; i < nums.length - 1; i++) {
            furthest = Math.max(furthest, i + nums[i]); // Update the furthest point
            if (i == currentEnd) { // If we've reached the end of the current jump range
                jumps++; // Increment the jump count
                currentEnd = furthest; // Update the end of the range for the next jump
                if (currentEnd >= nums.length - 1) { // If the end is beyond or at the last element, we're done
                    break;
                }
            }
        }
        return jumps;
    }
}
```
## Solution (Dynamic Programming) (Too slow)
```java
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;
        if (n == 1) return 0; // No jumps needed if there's only one element
        
        int[] dp = new int[n];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0; // Starting point requires 0 jumps

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j <= i + nums[i] && j < n; j++) {
                dp[j] = Math.min(dp[j], dp[i] + 1);
            }
        }

        return dp[n - 1];
    }
}
```
