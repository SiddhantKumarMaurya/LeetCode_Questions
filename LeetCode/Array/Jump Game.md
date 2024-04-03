# [Jump Game](https://leetcode.com/problems/jump-game/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Dynamic Programming`, `Greedy`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/0a66b6d9-e9ea-4a48-84d8-f61c0f3e54c0)
## Solution
```java
// Greedy Approach
class Solution {
    public boolean canJump(int[] nums) {
        int length = nums.length;
        int jumpFarthest = 0;

        for (int i = 0; i < length; i++) {
            if (jumpFarthest < i) return false;

            jumpFarthest = Math.max(jumpFarthest, i + nums[i]);

            if (jumpFarthest >= length - 1) return true;
        }
        return false;
    }
}
```
