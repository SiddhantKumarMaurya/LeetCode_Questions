# [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)
## Topics: `Array`, `Hash Table`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b07fb6ec-f4cc-47ec-866f-5ef4a766343e)
## Solution (Sorting)
```java
import java.util.Arrays;
class Solution {
    public boolean containsDuplicate(int[] nums) {
        int length = nums.length;
        Arrays.sort(nums);

        for (int i = 0; i < length - 1; i++) {
            if (nums[i] == nums[i + 1]) return true;
        }

        return false;
    }
}
```
---
## Solution (Hash Set)
`Takes less time than the above approach`
```java
import java.util.HashSet;

class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        
        for (int num : nums) {
            if (set.contains(num)) {
                return true; // Found a duplicate
            }
            set.add(num);
        }
        
        return false; // No duplicates found
    }
}
```
