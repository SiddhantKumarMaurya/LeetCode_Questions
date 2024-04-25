# [Longest Ideal Subsequence](https://leetcode.com/problems/longest-ideal-subsequence/description/?envType=daily-question&envId=2024-04-25)
## Topics: `Hash Table` `String`, `Dynamic Programming`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/facaaeb6-b70d-4f56-bb6d-65485306d625)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ab1e6c71-b8b9-4c73-9a8d-85114baa723a)
## Solution
```java
class Solution {
    
    public int longestIdealString(String s, int k) {
        
        int[] dp = new int[27];
        int n = s.length();
        
        for(int i = n-1; i >= 0 ;i--){
            char cc = s.charAt(i);
            int idx = cc - 'a';
            int max  = Integer.MIN_VALUE;
            
            int left = Math.max((idx-k), 0);
            int right = Math.min((idx + k), 26);
            
            for(int j = left; j <= right ; j++){
                max = Math.max(max, dp[j]);
            }
            
            dp[idx] = max+1;
        }
        
        int max = Integer.MIN_VALUE;
        
        for(int ele : dp){
            max = Math.max(ele, max);
        }
        
        return max;
    }
}
```
