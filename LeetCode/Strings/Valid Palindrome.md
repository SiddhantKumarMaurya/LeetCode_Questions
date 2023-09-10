# [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/7ece502f-e753-4df7-8422-6050de5af6eb)
## Solutions
### Java
``` java
class Solution {
    public boolean isPalindrome(String s) {
        // Convert the string to lowercase
        s = s.toLowerCase();
        
        // Remove all non-alphanumeric characters
        StringBuilder cleanString = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (Character.isLetterOrDigit(c)) {
                cleanString.append(c);
            }
        }
        
        // Check if it's a palindrome
        String original = cleanString.toString();
        String reversed = cleanString.reverse().toString();
        
        return original.equals(reversed);
    }
}
```
### Python
``` python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Convert the string to lowercase
        s = s.lower()

        # Remove all non-alphanumeric characters
        clean_string = ''.join(filter(str.isalnum, s))

        # Check if it's a palindrome
        return clean_string == clean_string[::-1]

```
### JavaScript
``` javascript
var isPalindrome = function(s) {
    // Convert the string to lowercase
    s = s.toLowerCase();

    // Remove all non-alphanumeric characters
    var cleanString = s.replace(/[^a-z0-9]/g, '');

    // Check if it's a palindrome
    return cleanString === cleanString.split('').reverse().join('');
};

```
### Lua
``` lua
function isPalindrome(s)
    -- Convert the string to lowercase
    s = string.lower(s)

    -- Remove all non-alphanumeric characters
    local cleanString = s:gsub('[^%w]', '')

    -- Check if it's a palindrome
    return cleanString == string.reverse(cleanString)
end

```
### C++
``` c++
#include <iostream>
#include <cctype>
using namespace std;

class Solution {
public:
    bool isPalindrome(string s) {
        // Convert the string to lowercase
        transform(s.begin(), s.end(), s.begin(), ::tolower);

        // Remove all non-alphanumeric characters
        string cleanString = "";
        for (char c : s) {
            if (isalnum(c)) {
                cleanString += c;
            }
        }

        // Check if it's a palindrome
        string reversed = cleanString;
        reverse(reversed.begin(), reversed.end());

        return cleanString == reversed;
    }
};

```
### C
``` c
#include <stdio.h>
#include <stdbool.h>
#include <ctype.h>
#include <string.h>

bool isPalindrome(char *s) {
    // Convert the string to lowercase
    for (int i = 0; s[i]; i++) {
        s[i] = tolower(s[i]);
    }

    int length = strlen(s);
    char cleanString[length + 1]; // +1 for null terminator
    int cleanIndex = 0;

    // Remove all non-alphanumeric characters
    for (int i = 0; s[i]; i++) {
        if (isalnum(s[i])) {
            cleanString[cleanIndex++] = s[i];
        }
    }
    cleanString[cleanIndex] = '\0';

    // Check if it's a palindrome
    int i = 0;
    int j = strlen(cleanString) - 1;
    while (i < j) {
        if (cleanString[i] != cleanString[j]) {
            return false;
        }
        i++;
        j--;
    }

    return true;
}

```
