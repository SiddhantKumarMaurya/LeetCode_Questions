# [Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/5b4f674d-0968-4643-8bbd-de66a72fa4d6)
## Solution
```java
class Solution {
    public int maxArea(int[] height) {
        int leftPointer = 0;
        int rightPointer = height.length - 1;
        int maxWater = 0;

        while (leftPointer < rightPointer) {
            int currentWater = Math.min(height[leftPointer], height[rightPointer]) * (rightPointer - leftPointer);
            maxWater = Math.max(maxWater, currentWater);

            // Move the pointer with the smaller height
            if (height[leftPointer] < height[rightPointer]) {
                leftPointer++;
            } else {
                rightPointer--;
            }
        }

        return maxWater;
    }
}
```
