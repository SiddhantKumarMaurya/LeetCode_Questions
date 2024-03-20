# [Is Subsequence](https://leetcode.com/problems/is-subsequence/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/bec48eb0-adde-429f-8bc7-b0902cc43f38)
## Solution
```java
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
```
## Solution for For Follow Up
``` java
import java.util.*;

public class SubsequenceChecker {
    public static boolean isSubsequence(String s, String t) {
        // Preprocess t to build an index for quick subsequence checks
        Map<Character, List<Integer>> index = new HashMap<>();
        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);
            index.putIfAbsent(c, new ArrayList<>());
            index.get(c).add(i);
        }

        int tPointer = 0; // Pointer for string t

        for (char c : s.toCharArray()) {
            if (!index.containsKey(c)) return false; // Character not found in t
            List<Integer> positions = index.get(c);
            int posIndex = Collections.binarySearch(positions, tPointer); // Binary search for next position
            if (posIndex < 0) posIndex = -(posIndex + 1); // If not found, get the insertion point
            if (posIndex == positions.size()) return false; // No more positions for this character in t
            tPointer = positions.get(posIndex) + 1; // Move tPointer to the next occurrence
        }

        return true;
    }

    public static void main(String[] args) {
        String t = "ahbgdc";
        System.out.println(isSubsequence("abc", t)); // Output: true
        System.out.println(isSubsequence("axc", t)); // Output: false
    }
}
```
