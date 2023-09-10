# [Add Strings](https://leetcode.com/problems/add-strings/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ec1213a3-f768-46ee-9127-d5a35d493262)
## Solutions
### Java
``` java
class Solution {
    public String addStrings(String num1, String num2) {
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        int carry = 0;
        StringBuilder result = new StringBuilder();

        while (i >= 0 || j >= 0) {
            int digit1 = (i >= 0) ? num1.charAt(i) - '0' : 0;
            int digit2 = (j >= 0) ? num2.charAt(j) - '0' : 0;
            int sum = digit1 + digit2 + carry;
            carry = sum / 10;
            result.append(sum % 10);
            i--;
            j--;
        }

        if (carry > 0) {
            result.append(carry);
        }

        return result.reverse().toString();
    }
}
```
### Python
``` python
class Solution:
    def addStrings(self, num1: str, num2: str) -> str:
        i, j = len(num1) - 1, len(num2) - 1
        carry = 0
        result = []

        while i >= 0 or j >= 0 or carry:
            digit1 = int(num1[i]) if i >= 0 else 0
            digit2 = int(num2[j]) if j >= 0 else 0
            _sum = digit1 + digit2 + carry
            carry = _sum // 10
            result.append(str(_sum % 10))
            i -= 1
            j -= 1

        return ''.join(result[::-1])

```
### JavaScript
``` javascript
var addStrings = function (num1, num2) {
    let i = num1.length - 1;
    let j = num2.length - 1;
    let carry = 0;
    let result = [];

    while (i >= 0 || j >= 0 || carry) {
        const digit1 = i >= 0 ? parseInt(num1[i]) : 0;
        const digit2 = j >= 0 ? parseInt(num2[j]) : 0;
        const sum = digit1 + digit2 + carry;
        carry = Math.floor(sum / 10);
        result.push(sum % 10);
        i--;
        j--;
    }

    return result.reverse().join('');
};

```
### Lua
``` lua
function addStrings(num1, num2)
    local i, j = #num1, #num2
    local carry = 0
    local result = {}

    while i >= 1 or j >= 1 or carry > 0 do
        local digit1 = i >= 1 and tonumber(num1:sub(i, i)) or 0
        local digit2 = j >= 1 and tonumber(num2:sub(j, j)) or 0
        local _sum = digit1 + digit2 + carry
        carry = math.floor(_sum / 10)
        table.insert(result, 1, _sum % 10)
        i = i - 1
        j = j - 1
    end

    return table.concat(result)
end

```
### C++
``` c++
#include <iostream>
using namespace std;

class Solution {
public:
    string addStrings(string num1, string num2) {
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        int carry = 0;
        string result;

        while (i >= 0 || j >= 0 || carry) {
            int digit1 = i >= 0 ? num1[i] - '0' : 0;
            int digit2 = j >= 0 ? num2[j] - '0' : 0;
            int _sum = digit1 + digit2 + carry;
            carry = _sum / 10;
            result += to_string(_sum % 10);
            i--;
            j--;
        }

        reverse(result.begin(), result.end());
        return result;
    }
};

```
### C
``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* addStrings(char* num1, char* num2) {
    int len1 = strlen(num1);
    int len2 = strlen(num2);
    int i = len1 - 1;
    int j = len2 - 1;
    int carry = 0;
    int resultSize = len1 > len2 ? len1 + 2 : len2 + 2; // +2 for result and null terminator
    char* result = (char*)malloc(resultSize);
    int resultIndex = 0;

    while (i >= 0 || j >= 0 || carry) {
        int digit1 = i >= 0 ? num1[i] - '0' : 0;
        int digit2 = j >= 0 ? num2[j] - '0' : 0;
        int _sum = digit1 + digit2 + carry;
        carry = _sum / 10;
        result[resultIndex++] = _sum % 10 + '0';
        i--;
        j--;
    }

    if (resultIndex == 0) {
        result[resultIndex++] = '0';
    }

    result[resultIndex] = '\0';
    // Reverse the result in-place
    for (int start = 0, end = resultIndex - 1; start < end; start++, end--) {
        char temp = result[start];
        result[start] = result[end];
        result[end] = temp;
    }

    return result;
}
```
