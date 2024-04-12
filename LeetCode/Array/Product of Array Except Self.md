# [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Prefix Sum`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b603dff5-1018-4fa2-ac62-8d6595d69cc5)
## Solution
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int length = nums.length;
        int[] prefix = new int[length];
        int[] suffix = new int[length];

        prefix[0] = 1;
        for (int i = 1; i < length; i++) {
            prefix[i] = prefix[i - 1] * nums[i - 1];
        }

        suffix[length - 1] = 1;
        for (int i = length - 2; i >= 0; i--) {
            suffix[i] = suffix[i + 1] * nums[i + 1];
        }

        int[] result = new int[length];

        for (int i = 0; i < length; i++) {
            result[i] = prefix[i] * suffix[i];
        }

        return result;
    }
}
```
