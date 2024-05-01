# [Reverse Prefix of Word](https://leetcode.com/problems/reverse-prefix-of-word/description/)
## Topics: `Two Pointers`, `String`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/6d73f1fb-d3c5-4521-b18f-700b0ca381df)
## Solution
```java
class Solution {
    public String reversePrefix(String word, char ch) {
        int length = word.length();
        StringBuilder str;
        int indexOfch = word.indexOf(ch);
        if (indexOfch < 0) return word;
        else {
            str = new StringBuilder(word.substring(0, indexOfch + 1));
            str.reverse();
        }
        str.append(word.substring(indexOfch + 1));
        return str.toString();
    }
}
```
