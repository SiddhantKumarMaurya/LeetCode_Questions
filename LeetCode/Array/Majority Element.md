# [Majority Element](https://leetcode.com/problems/majority-element/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/9d57d76a-57ba-4aff-bbac-b838bf74dffa)
## Solution
```java
class Solution {
    public int majorityElement(int[] nums) {
        int length = nums.length;
        int max = 0;
        int min = 0;
        int positiveMax = 0;
        int negativeMax = 0;

        for (int i = 0; i < length; i++) {
            if(nums[i] > max) {
                max = nums[i];
            }
            if(nums[i] < min) {
                min = nums[i];
            }
        }

        int positiveCount[] = new int[max + 1];
        int negativeCount[] = new int[-1*(min) + 1];

        for (int i = 0; i < length; i++) {
            if (nums[i] >= 0) {
                positiveCount[nums[i]]++;
            }
            else {
                negativeCount[-1*(nums[i])]++;
            }
        }

        for (int i = 0; i < max + 1; i++) {
            if (positiveCount[i] > (length / 2)) {
                return i;
            }
        }

        for (int i = 0; i < -1*min + 1; i++) {
            if (negativeCount[i] > (length / 2)) {
                return -1*i;
            }
        }
        return 0;
    }
}
```
---
## Solution
Sort the array and get the element at &fracn2 th index