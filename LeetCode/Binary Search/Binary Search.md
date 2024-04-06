# [Binary Search](https://leetcode.com/problems/binary-search/description/)
## Topics: `Array`, `Binary Search`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b730279f-0235-48a6-b707-90d47a63126a)
## Solution
```java
import java.util.Arrays;
class Solution {
    public int search(int[] nums, int target) {
// It returns the index of the search key if it is contained in the array; otherwise, it returns (-(insertion point) - 1). The insertion point is the index at which the key would be inserted into the array to maintain sorted order.
        int foundIndex = Arrays.binarySearch(nums, target);
        if (foundIndex > -1) return foundIndex;
        else return - 1;
    }
}
```
