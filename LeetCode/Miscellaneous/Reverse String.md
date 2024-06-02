# [Reverse String](https://leetcode.com/problems/reverse-string/description/?envType=daily-question&envId=2024-06-02)
## Topics: `Two Pointers`, `String`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ad4996c7-80ea-4c4a-96bc-fc9c82e806f7)
## Solution
```java
class Solution {
    public void reverseString(char[] s) {
        int length = s.length;
        for(int i = 0; i < length / 2; i++){
            char temp = s[i];
            s[i] = s[length - i - 1];
            s[length - i -1] = temp;
        }
    }
}
```
