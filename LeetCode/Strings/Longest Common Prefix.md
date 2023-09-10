# [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/62507238-3c37-4cc8-94e8-dd12c0a0de90)
## Solution
``` java
import java.util.Arrays;

class Solution {
    public String longestCommonPrefix(String[] strs) {
        int length = strs.length;

        // Handels corner cases
        if(length == 0) {
            return "";
        } else if (length == 1) {
            return strs[0];
        }

        // Sorts the provided String array
        Arrays.sort(strs);

        // Finds minimum lenght among the first and last string in the sorted array
        int minLength = Math.min(strs[0].length(), strs[length-1].length());

        // Finds all the common prefix
        int i = 0;
        while(i < minLength && strs[0].charAt(i) == strs[length-1].charAt(i)) {
            i++;
        }

        return strs[0].substring(0, i);
    }
}
```
