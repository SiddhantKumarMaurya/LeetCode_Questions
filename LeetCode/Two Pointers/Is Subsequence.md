# [Is Subsequence](https://leetcode.com/problems/is-subsequence/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/bec48eb0-adde-429f-8bc7-b0902cc43f38)
## Solution
class Solution {
    public boolean isSubsequence(String s, String t) {
        if (s.length() == 0) // An empty string is always a subsequence of any string
            return true;

        int sPointer = 0; // Pointer for string s
        int tPointer = 0; // Pointer for string t

        while (tPointer < t.length()) {
            if (s.charAt(sPointer) == t.charAt(tPointer)) {
                sPointer++; // Move sPointer to the next character in s
                if (sPointer == s.length()) // If all characters of s have been matched
                    return true;
            }
            tPointer++; // Move tPointer to the next character in t
        }

        return false;
    }
}
