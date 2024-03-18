# [Ransom Note](https://leetcode.com/problems/ransom-note/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d9a69965-5a8a-4c2c-a9d4-dc2754984c4f)
## Solution
```java
import java.util.HashMap;

class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if (ransomNote.length() > magazine.length()) return false;

        HashMap<Character, Integer> magazineChars = new HashMap<>();

        for (char c: magazine.toCharArray()) {
            magazineChars.put(c, magazineChars.getOrDefault(c, 0) + 1);
        }

        for (char c: ransomNote.toCharArray()) {
            if (!magazineChars.containsKey(c) || magazineChars.get(c) == 0)
                return false;

            magazineChars.put(c, magazineChars.get(c) - 1);
        }
        return true;
    }
}
```

## Solution (Reduced Time Complexity)
``` java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
		if (ransomNote.length() > magazine.length()) return false;
        int[] alphabets_counter = new int[26];
        
        for (char c : magazine.toCharArray())
            alphabets_counter[c-'a']++;

        for (char c : ransomNote.toCharArray()){
            if (alphabets_counter[c-'a'] == 0) return false;
            alphabets_counter[c-'a']--;
        }
        return true;
    }
}
```

## Another Possible Solution:
- Short both of the strings and compare till the length of ransomNote. If both the strings are same then return true and false otherwise.
