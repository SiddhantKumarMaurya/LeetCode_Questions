# [Single Number](https://leetcode.com/problems/single-number/)
## Problem Statement 
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/b2af7287-d276-4f0c-84b6-4f693705f129)
## Solution
```java
class Solution {
    public int singleNumber(int[] nums) {
        int len = nums.length;

        // To get the maximum and minimum element of the array
        // Maximum will be used to create an array of positive integers of size max + 1
        // Minimum will be used to create an array of negative integers (if they exist in
        // the array) of size (-min + 1) as min will always be negative in case of presence
        // of negative numbers
        int max = nums[0];
        int min = nums[0];

        // Get the maximum and minimum values
        for (int i = 0; i < len; i++) {
            if (nums[i] > max) {
                max = nums[i];
            }
            if (nums[i] < min) {
                min = nums[i];
            }
        }

        // <ake the min positive as an array can't have negative size
        if (min < 0) {
            min = 0 - min;
        }

        // Declare the two arrays
        // Both of these arrays have elements of array nums as their index
        // if they are repeted in nums then they will have a non-zero value
        int countPositive[] = new int[max + 1];
        int countNegative[] = new int[min + 1];

        // Initialize the count of each element in both the array as zero
        for (int i = 0; i <= max; i++) {
            countPositive[i] = 0;
        }

        for (int i = 0; i <= min; i++) {
            countNegative[i] = 0;
        }

        // check for each element and increment the value of their frequency (count) by one
        // if they are found in the array
        for (int i = 0; i < len; i++) {
            if(nums[i] >=0) {
                countPositive[nums[i]]++;
            }
            if(nums[i] <= 0) {
                // There can't be a negative index
                // For example for the element -7 the index should be 7 thus 0-7 will be
                // the index
                countNegative[0 - nums[i]]++;
            }
        }

        // To store the single one
        int singleOne;

        // To store the index of single one found in the auxiliary arrays
        int singleOneIndex = 0;
        for (int i = 0; i <= max; i++) {
            if (countPositive[i] == 1) {
                singleOneIndex = i;
            }
        }

        for (int i = 0; i <= min; i++) {
            if (countNegative[i] == 1) {
                // If the element is found in this auxiliary array we have to take the
                // take the negative value as we know that this array was ment to count
                // the frequency of negative elements
                singleOneIndex = -i;
            }
        }

        // Finally, the index of element 1 found in either of the auxiliary arrays is the
        // required value
        singleOne = singleOneIndex;
        return singleOne;
    }
}
```
