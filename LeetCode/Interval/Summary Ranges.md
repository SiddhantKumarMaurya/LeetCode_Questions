# [Summary Ranges](https://leetcode.com/problems/summary-ranges/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/1c299703-2714-4d26-a391-813740d1b33a)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b5fb8a48-e689-4eb2-a21b-ab039626ff1f)
## Solution
```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        int length = nums.length;
        List<String> list = new ArrayList<>();
        if (length == 1) {
            list.add(nums[0] + "");
            return list;
        }

        if (length == 0) {
            return list;
        }  

        int start = nums[0];
        int end = start;
        for (int i = 1; i < length; i++) {
            if (nums[i] == nums[i - 1] + 1) {
                end = nums[i];
            } else {
                if (start != end) {
                    list.add(start + "->" + end);
                } else list.add(start + "");
                start = nums[i];
                end = nums[i];
            }
        }

        // for the last index
        if (start != end) {
            list.add(start + "->" + end);
        } else list.add(start + "");
        
        return list;
    }
}
```
--- 
## Solution
```java

```
