# [Relative Ranks](https://leetcode.com/problems/relative-ranks/description/)
## Topics: `Array`, `Sorting`, `Heap (Priority Queue)`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/da9eef06-15a6-48bc-b448-646bbaaf07e1)
## Solution
```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

class Solution {
    public String[] findRelativeRanks(int[] score) {
        int n = score.length;
        String[] result = new String[n];

        // Create a map to store each athlete's original index
        Map<Integer, Integer> indexMap = new HashMap<>();
        for (int i = 0; i < n; i++) {
            indexMap.put(score[i], i);
        }

        // Sort the scores in descending order
        Arrays.sort(score);
        reverse(score);

        // Assign ranks
        for (int i = 0; i < n; i++) {
            int originalIndex = indexMap.get(score[i]);
            if (i == 0) {
                result[originalIndex] = "Gold Medal";
            } else if (i == 1) {
                result[originalIndex] = "Silver Medal";
            } else if (i == 2) {
                result[originalIndex] = "Bronze Medal";
            } else {
                result[originalIndex] = String.valueOf(i + 1);
            }
        }

        return result;
    }

    // Helper method to reverse an array
    private void reverse(int[] arr) {
        int left = 0, right = arr.length - 1;
        while (left < right) {
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }
}
```
---
## Solution
```java
import java.util.*;

class Solution {
    public String[] findRelativeRanks(int[] score) {
        int n = score.length;
        String[] result = new String[n];

        // Create a priority queue to store scores along with their indices
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[0] - a[0]); // Max heap

        // Populate the priority queue
        for (int i = 0; i < n; i++) {
            pq.offer(new int[]{score[i], i});
        }

        // Assign ranks
        int rank = 1;
        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int index = current[1];
            if (rank == 1) {
                result[index] = "Gold Medal";
            } else if (rank == 2) {
                result[index] = "Silver Medal";
            } else if (rank == 3) {
                result[index] = "Bronze Medal";
            } else {
                result[index] = String.valueOf(rank);
            }
            rank++;
        }

        return result;
    }
}
```
===
## Solution
```java

class Solution {
    public String[] findRelativeRanks(int[] score) {
        int n = score.length;
        int[] sortedScore = score.clone();
        Arrays.sort(sortedScore);
        String[] ranks = new String[n];
        
        for (int i = 0; i < n; i++) {
            int rank = Arrays.binarySearch(sortedScore, score[i]);
            if (rank == n - 1) {
                ranks[i] = "Gold Medal";
            } else if (rank == n - 2) {
                ranks[i] = "Silver Medal";
            } else if (rank == n - 3) {
                ranks[i] = "Bronze Medal";
            } else {
                ranks[i] = String.valueOf(n - rank);
            }
        }
        
        return ranks;
    }
}
```
