# [Get Equal Substrings Within Budget](https://leetcode.com/problems/get-equal-substrings-within-budget/description/)
## Topics: `String`, `Binary Search`, `Sliding Window`, `Prefix Sum`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/adbeed8f-2e42-4ad5-bc3d-5a2c3ca18ebe)
## Solution
```java
class Solution {
    public int equalSubstring(String s, String t, int maxCost) {
        int n = s.length();
        int start = 0, end = 0, currentCost = 0, maxLength = 0;

        while (end < n) {
            currentCost += Math.abs(s.charAt(end) - t.charAt(end));

            // If the current cost exceeds maxCost, move the start pointer to the right
            while (currentCost > maxCost) {
                currentCost -= Math.abs(s.charAt(start) - t.charAt(start));
                start++;
            }

            // Update the maximum length
            maxLength = Math.max(maxLength, end - start + 1);
            end++;
        }

        return maxLength;
    }
}
```
