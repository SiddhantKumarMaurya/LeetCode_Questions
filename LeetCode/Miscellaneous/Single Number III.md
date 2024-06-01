# [Single Number III](https://leetcode.com/problems/single-number-iii/description/?envType=daily-question&envId=2024-05-31)
## Topics: `Array`, `Bit Manipulation`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/5a810a6e-7b45-497e-bf3c-9916b80b7b08)
## Solution
```java
class Solution {
    public int[] singleNumber(int[] nums) {
        // Step 1: XOR all the numbers to get xorResult
        int xorResult = 0;
        for (int num : nums) {
            xorResult ^= num;
        }

        // Step 2: Find a set bit (rightmost set bit in xorResult)
        int setBit = xorResult & -xorResult;

        // Step 3: Initialize the two unique numbers
        int num1 = 0, num2 = 0;
        for (int num : nums) {
            if ((num & setBit) == 0) {
                num1 ^= num; // Belongs to the first group
            } else {
                num2 ^= num; // Belongs to the second group
            }
        }

        return new int[]{num1, num2};
    }
}
```
