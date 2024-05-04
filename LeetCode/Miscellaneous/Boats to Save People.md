# [Boats to Save People](https://leetcode.com/problems/boats-to-save-people/description/)
## Topics: `Array`, `Two Pointers`, `Greedy`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/7e075c94-fadd-4076-a9f8-479faf43cd8f)
## Solution (Initial Thought)
```java
import java.util.Arrays;
class Solution {
    public int numRescueBoats(int[] people, int limit) {
        int length = people.length;
        Arrays.sort(people);
        int numberOfBoats = 0;
        int totalWeight = 0;
        for (int i = 0; i < length;) {
            while (totalWeight <= limit && i < length) {
                totalWeight += people[i];
                i++;
            }
            numberOfBoats++;
            if (totalWeight > limit) {
                i--;
            }
            totalWeight = 0;
        }
        return numberOfBoats;
    }
}
/*
Failed for the following test case:
people = 5, 1, 4, 2
Output: 3
Expected output: 2
*/
```
---
## Solution
```java
import java.util.Arrays;

class Solution {
    public int numRescueBoats(int[] people, int limit) {
        Arrays.sort(people);
        int left = 0, right = people.length - 1;
        int boats = 0;
        
        while (left <= right) {
            if (people[left] + people[right] <= limit) {
                left++;
            }
            right--;
            boats++;
        }
        
        return boats;
    }
}
```
