# [Koko Eating Banana](https://leetcode.com/problems/koko-eating-bananas/description/)
## Topics: `Array`, `Binary Search`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/6cd8da1c-7bae-4a1b-a16f-fd45ee015359)
## Solution
```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        // Initialize the search range
        int left = 1;
        int right = Arrays.stream(piles).max().getAsInt();
        
        // Binary search loop
        while (left <= right) {
            // Calculate the middle eating speed
            int mid = left + (right - left) / 2;
            // we are taking long data type because
            // after adding large values the totalHours range increase
            // which later fails some of the test cases.
            long totalHours = 0;
            
            // Calculate total hours required to eat all bananas with current eating speed
            for (int pile : piles) {
                totalHours += (pile + mid - 1) / mid; // Divide pile by mid (rounded up)
                // lets say pile = 4, mid = 4
                // then if totalHours = (pile + mid) / mid;
                // totalHours = 2, is wrong.
                // it should be 1, so if totalHours = (pile + mid - 1) / mid;
                // then totalHours will be equal to 1 and near to 2 but not equal to 2
                // that's why the totalHours += (pile + mid - 1) / mid is correct.
            }
            
            // Adjust the search range based on total hours
            if (totalHours > h) {
                left = mid + 1; // If total hours exceed h, increase eating speed
            } else {
                right = mid - 1; // If total hours within h, decrease eating speed
            }
        }
        
        // Return the minimum eating speed found
        return left;
    }
}
```
