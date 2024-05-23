# [The Number of Beautiful Subsets](https://leetcode.com/problems/the-number-of-beautiful-subsets/description/)
## Topics: `Array`, `Dynamic Programming`, `Backtracking`, `Sorting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/afd5be04-7b31-4389-8ef4-6ccbf09d8851)
## Solution (Very Slow: Takes 5061ms and beats only 5.10% of players with Java)
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;

class Solution {
    public int beautifulSubsets(int[] nums, int k) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, nums, new ArrayList<>(), 0, k);
        return result.size();
    }

    private void backtrack(List<List<Integer>> result, int[] nums, List<Integer> currentSubset, int start, int k) {
        if (currentSubset.size() != 0 && isBeautifulSubset(currentSubset, k)) {
            result.add(new ArrayList<>(currentSubset));
        }

        for (int i = start; i < nums.length; i++) {
            currentSubset.add(nums[i]);
            backtrack(result, nums, currentSubset, i + 1, k);
            currentSubset.remove(currentSubset.size() - 1);
        }
    }

    private boolean isBeautifulSubset(List<Integer> subset, int k) {
        HashSet<Integer> set = new HashSet<>();
        for (int num: subset) {
            if(set.contains(num + k) || set.contains(num - k)) {
                return false;
            }
            set.add(num);
        }
        return true;
    }
}
```
---
## Solution (Very Slow: Takes 4420ms and beats only 5.10% of players with Java)
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;

class Solution {
    public int beautifulSubsets(int[] nums, int k) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, nums, new ArrayList<>(), 0, k);
        return result.size();
    }

    private void backtrack(List<List<Integer>> result, int[] nums, List<Integer> currentSubset, int start, int k) {
        if (currentSubset.size() != 0 && isBeautifulSubset(currentSubset, k)) {
            result.add(new ArrayList<>(currentSubset));
        }

        for (int i = start; i < nums.length; i++) {
            currentSubset.add(nums[i]);
            backtrack(result, nums, currentSubset, i + 1, k);
            currentSubset.remove(currentSubset.size() - 1);
        }
    }

    private boolean isBeautifulSubset(List<Integer> subset, int k) {
        // Copying is necessary, otherwise sorting will make changes to original subset
        // as a reference of subset is passed
        List<Integer> copySubset = new ArrayList<>(subset);
        Collections.sort(copySubset);
        int left = 0;
        int right = 1;
        int length = subset.size();
        
        while (right < length) {
            int diff = copySubset.get(right) - copySubset.get(left);
            
            if (diff == k) {
                return false;
            } else if (diff < k) {
                right++;
            } else {
                left++;
            }
            
            // Ensure the two pointers are not the same
            if (left == right) {
                right++;
            }
        }
        return true;
    }
}
```
---
## Solution (Very Slow: Takes 5491ms and beats only 5.10% of players with Java)
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int beautifulSubsets(int[] nums, int k) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, nums, new ArrayList<>(), 0, k);
        return result.size();
    }

    private void backtrack(List<List<Integer>> result, int[] nums, List<Integer> currentSubset, int start, int k) {
        if (currentSubset.size() > 0 && isBeautifulSubset(currentSubset, k)) {
            result.add(new ArrayList<>(currentSubset));
        }

        for (int i = start; i < nums.length; i++) {
            currentSubset.add(nums[i]);
            backtrack(result, nums, currentSubset, i + 1, k);
            currentSubset.remove(currentSubset.size() - 1);
        }
    }

    private boolean isBeautifulSubset(List<Integer> subset, int k) {
        for (int i = 0; i < subset.size(); i++) {
            for (int j = i + 1; j < subset.size(); j++) {
                if (Math.abs(subset.get(i) - subset.get(j)) == k) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
---
## Solution (Slow: Takes 652ms and only beats 39.26% of players with Java)
```java
import java.util.Arrays;

class Solution {
    public int beautifulSubsets(int[] nums, int k) {
        int n = nums.length;
        int maxMask = 1 << n; // 2^n possible subsets
        int[] dp = new int[maxMask]; // DP array to count subsets
        dp[0] = 1; // Base case: empty subset
        
        Arrays.sort(nums); // Sorting to ensure subsets are processed in order
        
        for (int i = 0; i < n; i++) {
            int num = nums[i];
            // Update DP array in reverse to avoid overwriting
            for (int mask = maxMask - 1; mask >= 0; mask--) {
                if (dp[mask] > 0) { // If this subset is valid
                    boolean canAdd = true;
                    for (int j = 0; j < n; j++) {
                        if ((mask & (1 << j)) != 0 && Math.abs(num - nums[j]) == k) {
                            canAdd = false;
                            break;
                        }
                    }
                    if (canAdd) {
                        dp[mask | (1 << i)] += dp[mask];
                    }
                }
            }
        }
        
        int result = 0;
        for (int mask = 1; mask < maxMask; mask++) {
            result += dp[mask];
        }
        
        return result;
    }
}
```
---
## Solution (Very Fast: 3ms and beats 100% of users with Java)
```java
class Solution {
    public int beautifulSubsets(int[] nums, int k) {
        
        Map<Integer, Integer> m = new HashMap<>();

        for (int num : nums) m.put(num, m.getOrDefault(num, 0) + 1);

        int res = 1, prev = 0, prevPrev = 0;

        for (Map.Entry<Integer, Integer> e : m.entrySet()) {
            int cur = e.getKey();

            if (m.containsKey(cur - k)) continue;
            
            prev = 0;

            while (m.containsKey(cur)) {
                prevPrev = prev;
                prev = ((1 << m.get(cur)) - 1) * res;
                res += prevPrev;
                cur += k;
            }
            res += prev;
        }
        return res - 1;
    }
}
```
