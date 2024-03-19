# [Word Pattern](https://leetcode.com/problems/word-pattern/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/7e168cb2-327a-46e5-bb65-5d433a16557f)
## Solution
```java
class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] words = s.split(" ");

        if (pattern.length() != words.length) return false;

        HashMap<Character, String> map = new HashMap<>();

        int length = pattern.length();

        for (int i = 0; i < length; i++) {
            // check for key value pair
            if (!map.containsKey(pattern.charAt(i))) {
                if (!map.containsValue(words[i])) {
                    // put key value pair
                    map.put(pattern.charAt(i), words[i]);
                } else return false;
            } else {
                if (!(map.get(pattern.charAt(i))).equals(words[i])) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
