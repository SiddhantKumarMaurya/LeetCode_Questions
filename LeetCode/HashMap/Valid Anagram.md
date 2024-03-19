# [Valid Anagram](https://leetcode.com/problems/valid-anagram/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/06654816-825f-4fb7-8fe0-70d5ef4cc736)
## Solution
```java
class Solution {
    public boolean isAnagram(String s, String t) {

        if (s.length() != t.length()) return false;
        HashMap<Character, Integer> map = new HashMap<>();

        int length = s.length();

        for (int i = 0; i < length; i++) {
            map.put(s.charAt(i), map.getOrDefault(s.charAt(i), 0) + 1);
        }

        for (int i = 0; i < length; i++) {
            if (!map.containsKey(t.charAt(i)) || map.get(t.charAt(i)) == 0) return false;
            else map.put(t.charAt(i), map.get(t.charAt(i)) - 1);
        }

        return true;
    }
}
```
