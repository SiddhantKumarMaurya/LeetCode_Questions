# [Score of a String](https://leetcode.com/problems/score-of-a-string/description/?envType=daily-question&envId=2024-06-01)
## Topics: `String`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c84878bb-c7ee-44c5-a574-159270df527f)
## Solution
```java
class Solution {
    public int scoreOfString(String s) {
        int score = 0;
        
        for (int i = 0; i < s.length() - 1; i++) {
            int asciiDiff = Math.abs(s.charAt(i) - s.charAt(i + 1));
            score += asciiDiff;
        }
 
        return score;
    }
}
```
