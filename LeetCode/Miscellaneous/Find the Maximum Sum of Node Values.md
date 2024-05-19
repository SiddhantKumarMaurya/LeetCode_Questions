# [Find the Maximum Sum of Node Values](https://leetcode.com/problems/find-the-maximum-sum-of-node-values/description/)
## Topics: `Array`, `Dynamic Programming`, `Greedy`, `Bit Manipulation`, `Tree`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ef115693-68a7-464d-a8b7-a9d8e7c853bf)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/6c0bd573-7c01-41fb-b078-662260108740)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/36e92524-31ab-489c-af34-ed561b27d337)
## Solution
```java
class Solution {
    public long maximumValueSum(int[] nums, int k, int[][] edges) {
        long total = 0;
        for (int num : nums) {
            total += num;
        }

        long totalDiff = 0;
        long diff;
        int positiveCount = 0;
        long minAbsDiff = Long.MAX_VALUE;
        for (int num : nums) {
            diff = (num ^ k) - num;

            if (diff > 0) {
                totalDiff += diff;
                positiveCount++;
            }
            minAbsDiff = Math.min(minAbsDiff, Math.abs(diff));
        }
        if (positiveCount % 2 == 1) {
            totalDiff -= minAbsDiff;
        }
        return total + totalDiff;
    }
}
```
---
## Solution
```java
class Solution {

    public long maximumValueSum(int[] nums, int k, int[][] edges) {
        
        long sum = 0;
        long minExtra = 1000000;
        int count = 0;

        for( int val : nums) {
            if ((val ^ k) > val ) {
                sum += val ^ k;
                minExtra = Math.min(minExtra, (val ^ k)- val);
                count++;
            } else {
                sum += val;
                minExtra = Math.min(minExtra, val - (val ^ k));
            }
        }

        if ( count %2 ==0 ) {
            return sum;
        } else {
            return sum - minExtra;
        }

    }
}
```
