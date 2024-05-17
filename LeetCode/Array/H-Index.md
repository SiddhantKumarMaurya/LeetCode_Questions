# [H-Index](https://leetcode.com/problems/h-index/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Sorting`, `Counting Sort`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/392c8937-edd0-4ca0-aee3-2e73d4934996)
## Solution:
```java
import java.util.Arrays;

public class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        int n = citations.length;
        
        for (int i = 0; i < n; i++) {
            int h = n - i; // h is the number of papers with at least citations[i] citations
            if (citations[i] >= h) {
                return h;
            }
        }
        
        return 0;
    }
}
```
