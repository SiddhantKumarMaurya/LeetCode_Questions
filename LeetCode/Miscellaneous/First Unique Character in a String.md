# [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/description/)
## Topics: `Hash Table`, `String`, `Queue`, `Counting`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/9c1a7ad8-9ae7-4641-8f48-5aa0a65f8319)
## Solution
```java
import java.util.HashMap;
class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> mapCount = new HashMap<>();
        HashMap<Character, Integer> mapIndex = new HashMap<>();
        int length = s.length();
        for (int i = 0; i < length; i++) {
            char letter = s.charAt(i);
            mapCount.put(letter, mapCount.getOrDefault(letter, 0) + 1);
            mapIndex.put(letter, i);
        }

        for (int i = 0; i < length; i++) {
            char letter = s.charAt(i);
            if (mapCount.get(letter) == 1) return mapIndex.get(letter);
        }
        return -1;
    }
}
```
---
## Solution
```java
class Solution {
    public int firstUniqChar(String s) {
    int arr[]=new int[26];
    char ch[]=s.toCharArray();
    for(int i=0;i<ch.length;i++)
    arr[ch[i]-'a']++;
    for(int i=0;i<ch.length;i++)
     if(arr[ch[i]-'a']==1)return i;
     return -1;
    }
}
```
