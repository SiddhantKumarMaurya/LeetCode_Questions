# [Freedom Trail](https://leetcode.com/problems/freedom-trail/description/)
## Topics: `String`, `Dynamic Programming`, `Depth-First Search`, `Breadth-First Search`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/86266092-12dc-4553-b795-0d8d8557404a)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/1ed42e19-ff99-40d7-b615-fd429c77cf7b)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ca8d02ed-8291-488e-bde0-e56c4326bba8)
## Solution
```java
import java.util.*;

public class Solution {
    public int findRotateSteps(String ring, String key) {
        int n = ring.length();
        int m = key.length();
        // Map to store the indices of each character in the ring
        Map<Character, List<Integer>> charIndices = new HashMap<>();
        for (int i = 0; i < n; i++) {
            char c = ring.charAt(i);
            charIndices.computeIfAbsent(c, k -> new ArrayList<>()).add(i);
        }
        // Dynamic programming array to store minimum steps required to align characters
        int[][] dp = new int[m][n];
        for (int[] row : dp) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        // Initialize the starting position
        for (int idx : charIndices.get(key.charAt(0))) {
            dp[0][idx] = Math.min(idx, n - idx) + 1; // Add one step for pressing the center button
        }
        // Iterate through each character in the key
        for (int j = 1; j < m; j++) {
            // Iterate through all possible rotations of the ring
            for (int idx : charIndices.get(key.charAt(j))) {
                // Find the minimum steps required to align the current character of the ring with the current character of the key
                for (int prevIdx : charIndices.get(key.charAt(j - 1))) {
                    int steps = Math.min(Math.abs(idx - prevIdx), n - Math.abs(idx - prevIdx)) + 1; // Add one step for pressing the center button
                    dp[j][idx] = Math.min(dp[j][idx], dp[j - 1][prevIdx] + steps);
                }
            }
        }
        // Find the minimum steps required to align the last character of the key with any character in the ring
        int minSteps = Integer.MAX_VALUE;
        for (int steps : dp[m - 1]) {
            minSteps = Math.min(minSteps, steps);
        }
        return minSteps;
    }
}
```
