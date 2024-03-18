# [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b1427591-bcd1-493a-a4e4-b493f2799bca)
## Solution
``` java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) return false;

        // make a character array for each string
        char[] s_array = s.toCharArray();
        char[] t_array = t.toCharArray();

        // for the mapping of the characters
        HashMap<Character, Character> mapCharacters = new HashMap<>();

        int length = s_array.length;
        for (int i = 0; i < length; i++) {

            // if a key is not present
            if (!mapCharacters.containsKey(s_array[i])) {
                // if the value is not present
                if (!mapCharacters.containsValue(t_array[i])) {
                    // add the key value pair
                    mapCharacters.put(s_array[i], t_array[i]);
                } else return false;
            } else {
                // if the key value pair mismatch
                if (mapCharacters.get(s_array[i]) != t_array[i]) return false;
            }
        }
        return true;
    }
}
```
