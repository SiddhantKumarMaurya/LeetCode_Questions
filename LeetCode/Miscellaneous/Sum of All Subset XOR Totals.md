# [Sum of All Subset XOR Totals](https://leetcode.com/problems/sum-of-all-subset-xor-totals/description/?envType=daily-question&envId=2024-05-20)
## Topics: `Array`, `Math`, `Backtracking`, `Bit Manipulation`, `Combinatorics`, `Enumeration`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/14f94b1f-9656-4e60-81d1-365cb60c0500)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b4dc068d-642e-49b3-807e-acd723bea0f8)
## Solution
```java
class Solution {
    public int subsetXORSum(int[] nums) {
        return calculateXORSum(nums, 0, 0);
    }
    
    private int calculateXORSum(int[] nums, int index, int currentXOR) {
        if (index == nums.length) {
            return currentXOR;
        }
        
        // Calculate XOR sum including the current element
        int include = calculateXORSum(nums, index + 1, currentXOR ^ nums[index]);
        // Calculate XOR sum excluding the current element
        int exclude = calculateXORSum(nums, index + 1, currentXOR);
        
        // Return the sum of both cases
        return include + exclude;
    }
}
```
