## [Append Characters to String to Make Subsequence](https://leetcode.com/problems/append-characters-to-string-to-make-subsequence/description/)
## Topics: `Two Pointers`, `String`, `Greedy`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d0465e8b-4bdb-48d3-ba23-63eec36148cc)
## Solution
```java
class Solution {
    public int appendCharacters(String s, String t) {
        int maxIndexMatch = 0;
        int length = s.length();
        int slength = t.length();

        for (int i = 0; i < length; i++) {
            try {
                if (s.charAt(i) == t.charAt(maxIndexMatch)) {
                    maxIndexMatch++;
                }
              // When t is already a subsequence of s or t.length < s.length
            } catch (StringIndexOutOfBoundsException e) {
                return 0;
            }
        }
        return slength - maxIndexMatch;
    }
}
```
