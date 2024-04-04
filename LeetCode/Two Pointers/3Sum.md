# [3Sum](https://leetcode.com/problems/3sum/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Two Pointers`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c558e877-8f37-43b5-8fc5-c4ec0b24912e)
### *Another Way to solve: Try using HashSet*
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
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums); // Sort the array
        List<List<Integer>> result = new ArrayList<>();

        for (int i = 0; i < nums.length - 2; i++) {
            if (i == 0 || (i > 0 && nums[i] != nums[i - 1])) { // Skip duplicates
                int left = i + 1, right = nums.length - 1, target = -nums[i];
                while (left < right) {
                    if (nums[left] + nums[right] == target) {
                        result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                        while (left < right && nums[left] == nums[left + 1]) left++; // Skip duplicates
                        while (left < right && nums[right] == nums[right - 1]) right--; // Skip duplicates
                        left++;
                        right--;
                    } else if (nums[left] + nums[right] < target) {
                        left++;
                    } else {
                        right--;
                    }
                }
            }
        }

        return result;
    }
}
```
