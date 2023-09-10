# [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c0ded6f2-b08f-4ccf-be39-5b9696bb79df)
## Solution (Java)
``` java
class Solution {
    public int myAtoi(String s) {
        int length = s.length();
        int i = 0;

        // Skip leading spaces
        while (i < length && s.charAt(i) == ' ') {
            i++;
        }

        if (i == length) {
            // String contains only spaces
            return 0;
        }

        char sign = '+';
        if (s.charAt(i) == '+' || s.charAt(i) == '-') {
            sign = s.charAt(i);
            i++;
        }

        long result = 0; // Using long for range checking
        while (i < length && Character.isDigit(s.charAt(i))) {
            /*'0' is subtracted from the character at s.charAt(i). In Unicode/ASCII character
             encoding, characters '0' through '9' are contiguous, so subtracting '0' from any
             of these characters will yield the integer value of the digit.
            */
            int digit = s.charAt(i) - '0';
            result = result * 10 + digit;

            // Check for integer overflow
            if (result > Integer.MAX_VALUE) {
                return (sign == '-') ? Integer.MIN_VALUE : Integer.MAX_VALUE;
            }

            i++;
        }

        if (sign == '-') {
            result = -result;
        }

        return (int) result;
    }
}
```

## Solution(Python)
``` python
class Solution:
    def myAtoi(self, s: str) -> int:
        length = len(s)
        i = 0

        # Skip leading spaces
        while i < length and s[i] == ' ':
            i += 1

        if i == length:
            # String contains only spaces
            return 0

        sign = '+'
        if s[i] == '+' or s[i] == '-':
            sign = s[i]
            i += 1

        result = 0
        while i < length and s[i].isdigit():
            # ord() to get the Unicode code point of a character and - ord('0') 
            # to convert a  character representing a digit to its integer value.
            digit = ord(s[i]) - ord('0')
            result = result * 10 + digit

            # Check for integer overflow
            if result > 2147483647:
                return -2147483648 if sign == '-' else 2147483647

            i += 1

        if sign == '-':
            result = -result

        return result
```
