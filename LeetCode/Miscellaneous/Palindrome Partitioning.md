# [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/description/)
## Topics: `String`, `Dynamic Programming`, `Backtracking`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/990c6057-af46-4119-a073-adbd7a7f7561)
## Solution
```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), s, 0);
        return result;
    }

    private void backtrack(List<List<String>> result, List<String> current, String s, int start) {
        if (start == s.length()) {
            result.add(new ArrayList<>(current));
            return;
        }

        for (int end = start + 1; end <= s.length(); end++) {
            if (isPalindrome(s, start, end - 1)) {
                current.add(s.substring(start, end));
                backtrack(result, current, s, end);
                current.remove(current.size() - 1);
            }
        }
    }

    private boolean isPalindrome(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
        
        // No direct reverse funtion for strings in java
        // return s.equals(s.reverse());
    }
}
```
