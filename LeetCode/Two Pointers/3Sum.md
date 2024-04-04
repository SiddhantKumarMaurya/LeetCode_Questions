# [3Sum](https://leetcode.com/problems/3sum/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Two Pointers`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c558e877-8f37-43b5-8fc5-c4ec0b24912e)
## Solution (Incorrect)
```java
import java.util.List;
import java.util.ArrayList;
import java.util.Arrays;
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        int length = nums.length;
        Arrays.sort(nums);
        for (int i = 0; i < length; i++) {
            if (i < length && i + 1 < length && i + 2 < length) {
                if (nums[i] + nums[i + 1] + nums[i + 2] == 0) {
                    ArrayList<Integer> arrayList = new ArrayList<>();
                    arrayList.add(nums[i]);
                    arrayList.add(nums[i + 1]);
                    arrayList.add(nums[i + 1]);
                    list.add(arrayList);
                    i = i + 3;
                }
            }
        }
        return list;
    }
}
```
---
```java
```
