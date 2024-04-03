# [Candy](https://leetcode.com/problems/candy/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Greedy`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/f603ec9c-4b9f-4255-845d-6a7d742718a3)
## Solution (Incorrect)
```java
import java.util.Arrays;
class Solution {
    public int candy(int[] ratings) {
        int length = ratings.length;
        int[] candies = new int[length];
        Arrays.fill(candies, 1); // Time Complexity: O(n)
        for (int i = 0; i < length; i++) {
            if (i == length - 1) {
                if (ratings[i] > ratings[i - 1]) {
                    candies[i] = candies[i - 1] + 1;
                }
                break;
            }
            if (i >= 1) {
                if (ratings[i] > ratings[i - 1]) {
                    candies[i] = candies[i - 1] + 1;
                } else if (ratings[i] > ratings[i + 1]) {
                    candies[i] = candies[i + 1] + 1;
                } else if (ratings[i] > ratings[i - 1] && ratings[i] > ratings[i + 1]) {
                    candies[i] = Math.max(candies[i - 1], candies[i + 1]) + 1;
                }
            }
            else if (ratings[i] > ratings[i + 1]) {
                candies[i] = candies[i + 1] + 1;
            }
        }
        return Arrays.stream(candies).sum(); // Time Complexity: O(n)
    }
}
```
---
## Solution
```java
import java.util.Arrays;
class Solution {
    public int candy(int[] ratings) {
        int length = ratings.length;
        int[] candies = new int[length];
        candies[0] = 1;
        for (int i = 1; i < length; i++) {
            if (ratings[i] > ratings[i - 1]) candies[i] = candies[i - 1] + 1;
            else candies[i] = 1;
        }

        int totalCandies = candies[length - 1];
        for (int i = length - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                candies[i] = Math.max(candies[i], candies[i + 1] + 1);
            }
            totalCandies += candies[i];
        }
        return totalCandies;
    }
}
```
