# [Roman to Integer](https://leetcode.com/problems/roman-to-integer/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d2544d75-219d-453b-8909-1868cbe831e4)
## Solution
``` java
class Solution {
    public static int convertToInt(char c) {
        switch(c) {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
        }
        return 0;
    }
    public int romanToInt(String s) {
        int length = s.length();
        int sum = 0;
        for (int i = 0; i<length; i++) {
            int num = convertToInt(s.charAt(i));
            int nextNum;

            // To avoid index out of bound exception
            if (i+1 == length) {
                nextNum = 0;
            } else {
                nextNum = convertToInt(s.charAt(i+1));
            }
            
            if(num < nextNum) {
                sum = sum + nextNum - num;
                i++;
            } else {
                sum = sum + num;
            }
        }
        return sum;
    }
}
```
