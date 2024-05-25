# [Word Break II](https://leetcode.com/problems/word-break-ii/description/)
## Topics: `Array`, `Hash Table`, `String`, `Dynamic Programming`, `Backtracking`, `Trie`, `Memoization`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/e7470753-7b92-4003-9aa3-23cc503d3c0d)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/a61e5c30-265d-4ec5-bd9c-fc0534f89fb4)
## Solution (Very Slow: Takes 148ms and beats only 7.84% of users with Java)
```java
import java.util.List;
import java.util.HashSet;

class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        List<String> result = new ArrayList<>();
        // the following two lines of code do the same
        // make a set out of list
        HashSet<String> dict = new HashSet<>(wordDict);
        // dict.addAll(list);
        String str = "";
        String finalStr = "";
        backtrack(result, s, dict, 0, str, finalStr);
        return result;
    }

    private void backtrack(List<String> result, String s, HashSet<String> dict, int start, String currentStr, String finalStr) {
        int length = s.length();
        if (dict.contains(currentStr)) {
            finalStr += currentStr + " ";
            currentStr = "";
            if (start == length) {
                finalStr = finalStr.trim();
                if (!result.contains(finalStr)) {
                    result.add(finalStr);
                }
                System.out.println(result);
            }
        }
        
        for (int i = start; i < length; i++) {
            currentStr = currentStr + s.charAt(i);
            backtrack(result, s, dict, i + 1, currentStr, finalStr);
        }
    }
}
```
---
## Solution (Even more slow: Takes 305ms and beats only 7.84% of users with Java)
```java
import java.util.List;

class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        List<String> result = new ArrayList<>();
        String str = "";
        String finalStr = "";
        backtrack(result, s, wordDict, 0, str, finalStr);
        return result;
    }

    private void backtrack(List<String> result, String s, List<String> dict, int start, String currentStr, String finalStr) {
        int length = s.length();
        if (dict.contains(currentStr)) {
            finalStr += currentStr + " ";
            currentStr = "";
            if (start == length) {
                finalStr = finalStr.trim();
                if (!result.contains(finalStr)) {
                    result.add(finalStr);
                }
                System.out.println(result);
            }
        }
        
        for (int i = start; i < length; i++) {
            currentStr = currentStr + s.charAt(i);
            backtrack(result, s, dict, i + 1, currentStr, finalStr);
        }
    }
}
```
---
## Solution (Significantly faster than above approaches, but not too fast. Takes 6ms and beats only 15.41% users with Java)
```java
import java.util.List;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.HashMap;
import java.util.Set;
import java.util.Map;

class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);
        Map<String, List<String>> memo = new HashMap<>();
        return backtrack(s, dict, memo);
    }

    private List<String> backtrack(String s, Set<String> dict, Map<String, List<String>> memo) {
        if (memo.containsKey(s)) {
            return memo.get(s);
        }

        List<String> result = new ArrayList<>();
        if (s.length() == 0) {
            result.add("");
            return result;
        }

        for (String word : dict) {
            if (s.startsWith(word)) {
                String remaining = s.substring(word.length());
                List<String> subResult = backtrack(remaining, dict, memo);
                for (String sub : subResult) {
                    String optionalSpace = sub.isEmpty() ? "" : " ";
                    result.add(word + optionalSpace + sub);
                }
            }
        }

        memo.put(s, result);
        return result;
    }
}
```
## Solution (Fastest: Takes 1ms and beats 94.29% of users with Java)
```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> wordSet = new HashSet<>(wordDict);
        List<String> results = new ArrayList<>();
        backtrack(s, wordSet, new StringBuilder(), results, 0);
        return results;
    }

    private static void backtrack(String s, Set<String> wordSet, StringBuilder currentSentence, List<String> results,
            int startIndex) {
        if (startIndex == s.length()) {
            results.add(currentSentence.toString().trim());
            return;
        }

        for (int endIndex = startIndex + 1; endIndex <= s.length(); endIndex++) {
            String word = s.substring(startIndex, endIndex);
            if (wordSet.contains(word)) {
                int currentLength = currentSentence.length();
                currentSentence.append(word).append(" ");
                backtrack(s, wordSet, currentSentence, results, endIndex);
                currentSentence.setLength(currentLength);
            }
        }
    }
}
```
