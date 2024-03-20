# [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d9435216-cd6c-492e-a3ce-52d63ece5738)
## Solution (using HashSet) (time taken: 27 ms)
```java
import java.util.HashSet;
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        HashSet<Integer> numSet = new HashSet<>();
        
        for (int num: nums) numSet.add(num);

        int longestSequence = 0;
        for (int num: numSet) {
            if (!numSet.contains(num - 1)) {
                int currentNum = num;
                int currentSequence = 1;
                while (numSet.contains(currentNum + 1)) {
                    currentSequence++;
                    currentNum++;
                }
                longestSequence = Math.max(longestSequence, currentSequence);
            }  
        }
        return longestSequence;
    }
}
```
## Solution (using HashMap) (time taken: 1063 ms)
```java
import java.util.HashMap;
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        HashMap<Integer, Integer> numMap = new HashMap<>();
        
        for (int num: nums) {
            // if the key is not there it will be added with a value 1
            // if its there it will be overwritten
            numMap.put(num, 1);
        }

        int longestSequence = 0;
        for (int num: nums) {
            if (!numMap.containsKey(num - 1)) {
                int currentNum = num;
                int currentSequence = 1;
                while (numMap.containsKey(currentNum + 1)) {
                    currentSequence++;
                    currentNum++;
                }
                longestSequence = Math.max(longestSequence, currentSequence);
            }  
        }
        return longestSequence;
    }
}
```
