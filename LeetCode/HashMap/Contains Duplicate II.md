# [Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Hash Table`, `Sliding Window`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/32db1d59-3c8b-4710-ac32-51a4348d5f5f)
## Solution
```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int length = nums.length;

        for (int i = 0; i < length; i++) {
            if (map.containsKey(nums[i])) {
                if (Math.abs(map.get(nums[i]) - i) <= k) return true;
                map.put(nums[i], i);
            } else {
                map.put(nums[i], i);
            }
        }
        return false;
    }
}
```
---
## Solution (This one takes less time than the above one)
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> indexMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            if (indexMap.containsKey(num) && i - indexMap.get(num) <= k) {
                return true;
            }
            indexMap.put(num, i);
        }
        return false;
    }
}
```
---
## Solution (Sliding Window)
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> window = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            if (window.contains(nums[i])) {
                return true;
            }
            window.add(nums[i]);
            if (window.size() > k) {
                window.remove(nums[i - k]);
            }
        }
        return false;
    }
}
```
---
## Solution 
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i]) && i - map.get(nums[i]) <= k) {
                return true;
            }
            map.put(nums[i], i);
        }
        return false;
    }
}
```
--- 
## Solution
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k <= 0) {
            return false;
        }
        
        int n = nums.length;
        Set<Integer> window = new HashSet<>();
        
        for (int i = 0; i < n; i++) {
            if (i > k) {
                window.remove(nums[i - k - 1]); // Remove the leftmost element from the window
            }
            if (window.contains(nums[i])) { // Check if the current element already exists in the window
                return true;
            }
            window.add(nums[i]); // Add the current element to the window
        }
        
        return false;
    }
}
```
