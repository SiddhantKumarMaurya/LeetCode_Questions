# [Remove duplicates from Shorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/01f699ab-c7bb-4dcb-a932-02f394fc7418)
## Solution
``` java
class Solution {
    public int removeDuplicates(int[] nums) {
      int length = nums.length;

      // k keeps tracks of unique number and
      // also works as indices of unique numbers
      // since, the minimum length of the given array is 1
      // we can initialize k to 1
      int k = 1;

      for (int i = 0; i < length - 1; i++) {

        // when a duplicate is found the loop continues
        // without making any changes to the array
        // when unique number is found that number is stored 
        // at the index (k) 
        if (nums[i] == nums[i + 1]){
          continue;
        } else {
          nums[k] = nums[i + 1];
          k++;
        }
      }
      return k; 
    }
}
```
