# [Maximize Happiness of Selected Children](https://leetcode.com/problems/maximize-happiness-of-selected-children/description/?envType=daily-question&envId=2024-05-09)
## Topics: `Array`, `Greedy`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/0e5c7cb4-cfcf-42df-a98b-813cf9fdc130)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/e9667cf3-1a92-4cb5-8fb4-f6d01171ebdf)
## Solution
```java
class Solution {
    public long maximumHappinessSum(int[] happiness, int k) {
        Arrays.sort(happiness);
        long res = 0;
        int n = happiness.length, j = 0;

        for (int i = n - 1; i >= n - k; --i) {
            happiness[i] = Math.max(happiness[i] - j++, 0);
            res += happiness[i];
        }
        return res;
    }
}
```
