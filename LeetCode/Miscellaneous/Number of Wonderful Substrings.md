# [Number of Wonderful Substrings](https://leetcode.com/problems/number-of-wonderful-substrings/description/)
## Topics: `Hash Table`, `String`, `Bit Manipulation`, `Prefix Sum`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/9b39a2b0-5956-49f0-bc68-c87dad130f45)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/2ec11d4a-d713-4d9e-8abf-7ef8f6d3a398)
## Solution
```java
class Solution {
    public long wonderfulSubstrings(String word) {
        int[] count = new int[1024]; // Bitmask to represent the count of each character
        count[0] = 1; // Empty string has a wonderful substring
        
        long result = 0;
        int bitmask = 0;
        
        for (char ch : word.toCharArray()) {
            bitmask ^= 1 << (ch - 'a'); // Toggle the bit for the current character
            
            // For each possible prefix where one character count is odd and the rest are even,
            // add the count of wonderful substrings starting from that prefix.
            result += count[bitmask];
            
            // For each possible mask where one character count is odd and the rest are even,
            // add the count of wonderful substrings where the odd character is at position i.
            for (int i = 0; i < 10; i++) {
                result += count[bitmask ^ (1 << i)];
            }
            
            count[bitmask]++;
        }
        
        return result;
    }
}
```
