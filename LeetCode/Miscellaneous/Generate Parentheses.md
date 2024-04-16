# [Generate Parantheses](https://leetcode.com/problems/generate-parentheses/submissions/1233891250/)
## Topics: `String`, `Dynamic Programming`, `Backtracking`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/89929238-9674-48d9-8054-e3dbf74b0916)
## Solution
```java
import java.util.*;

class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, "", 0, 0, n);
        return result;
    }
    
    private void backtrack(List<String> result, String current, int open, int close, int max) {
        if (current.length() == max * 2) {
            result.add(current);
            return;
        }
        
        if (open < max) {
            backtrack(result, current + "(", open + 1, close, max);
        }
        if (close < open) {
            backtrack(result, current + ")", open, close + 1, max);
        }
    }
}
```
---
## Solution
```java
class Solution {
    public List<String> generateParenthesis(int n) {

        List<String> list = new ArrayList<>();

        if (n < 0 || n == 0) {
            return list;
        }

        StringBuilder str = new StringBuilder();

        helper(0, 0, n, str, list);
        return list;
    }

    public static void helper(int open, int close, int n, StringBuilder str, List<String> list) {

        if (close == n) {
            list.add(str.toString());
            return;
        }

        if (open < n) {

            str.append('(');
            helper(open + 1, close, n, str, list);
            str.deleteCharAt(str.length() - 1);
        }

        if (close < open) {
            str.append(')');
            helper(open, close + 1, n, str, list);
            str.deleteCharAt(str.length() - 1);

        }
    }
}
```
---
## Solution
```java
class Solution {

    List<String> res = new ArrayList<>();

    public List<String> generateParenthesis(int n) {
        helper(new StringBuilder("("), 1, n);
        return res;
    }

    public void helper(StringBuilder sb, int bracketsDiff, int n) {
        if (sb.length()+bracketsDiff > n*2) return;
        if (sb.length() == n*2 && bracketsDiff == 0) {
            res.add(sb.toString());
            return;
        }
        if (bracketsDiff < n) helper(new StringBuilder(sb).append('('), bracketsDiff + 1, n);
        if (bracketsDiff > 0) helper(new StringBuilder(sb).append(')'), bracketsDiff - 1, n);
    }
}
```
