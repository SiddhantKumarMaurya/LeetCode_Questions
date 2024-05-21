# [Subsets](https://leetcode.com/problems/subsets/description/)
## Topics: `Array`, `Backtracking`, `Bit Manipulation`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/9ed3e36d-d0cd-419e-ba3b-1dcfbb060a6b)
## Solution
```java
import java.util.List;
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, new ArrayList<>(), 0, result);
        return result;
    }        
    private void backtrack(int[] nums, List<Integer> current, int index, List<List<Integer>> result) {
        result.add(new ArrayList<>(current));

        for (int i = index; i < nums.length; i++) {
            current.add(nums[i]);
            backtrack(nums, current, i + 1, result);
            current.remove(current.size() - 1);
        }
    }
}
```
