# [Multiply Strings](https://leetcode.com/problems/multiply-strings/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/bbf155d3-4888-4647-9a8b-d72a94ac836d)
## Solutions:
### Initial Solution
##### I tried to solve it using ArrayList but it did not work at the moment. There was some error in my logic. (Need to solve it)
``` java
import java.util.ArrayList;

class Solution {
    public String multiply(String num1, String num2) {
        int len1 = num1.length();
        int len2 = num2.length();
        ArrayList<Integer> result = new ArrayList<Integer>(len1 + len2);

        for (int i = 0; i < len1 + len1; i++) {
            result.add(0);
        }
        int multiplicant, multiplier, multiple;
        for (int i = len1 - 1; i >= 0; i--) {
            int j = len2 - 1;
            int k = (len1 - 1) - i;
            while (j >= 0) {
                multiplicant = Integer.parseInt("" + num2.charAt(j));
                multiplier = Integer.parseInt("" + num1.charAt(i));
                multiple = multiplicant * multiplier + result.get(i + j + 1);
                result.set(i + j + 1, multiple % 10);
                result.set(i + j + 1, multiple / 10);
                j--;
            }
        }
       
        int size = result.size();
        String finalResult = "";
        boolean leadingZeroes = result.get(size - 1) == 0 ? true : false;
        for (int l = size - 1; l >= 0; l--) {
            if (leadingZeroes) {
                if (result.get(l) == 0) {
                    continue;
                } 
                else {
                    leadingZeroes = false;
                    l++;
                }
            } 
            else {
                    finalResult = finalResult + result.get(l);
            }
        }
        return finalResult;
    }    
}
```
### Correct Solutions:
### Java
``` java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

class Solution {
    public String multiply(String num1, String num2) {
        int len1 = num1.length();
        int len2 = num2.length();
        int[] result = new int[len1 + len2];

        for (int i = len1 - 1; i >= 0; i--) {
            for (int j = len2 - 1; j >= 0; j--) {
                int digit1 = num1.charAt(i) - '0';
                int digit2 = num2.charAt(j) - '0';
                int product = digit1 * digit2;
                // result[i + j + 1] represents the current accumulated value at 
                // the position i + j + 1 in the result array
                int sum = product + result[i + j + 1];
                result[i + j + 1] = sum % 10;
                result[i + j] += sum / 10;
            }
        }

        StringBuilder sb = new StringBuilder();
        for (int digit : result) {
            if (!(sb.length() == 0 && digit == 0)) {
                sb.append(digit);
            }
        }

        return sb.length() == 0 ? "0" : sb.toString();
    }
}

/* Some StringBuilder properties:
`StringBuilder` is a class in Java that is used to create and manipulate mutable sequences of characters. It is part of the `java.lang` package and is particularly useful when you need to concatenate or modify strings frequently.

Here's what `StringBuilder` does and why it's useful:

1. **Mutable**: Unlike `String` objects in Java, which are immutable (cannot be changed after creation), `StringBuilder` allows you to modify the contents of the string it represents. This can be more efficient when you need to build or modify a string in a loop or through multiple operations.

2. **Efficient**: `StringBuilder` is designed for efficiency when performing string concatenation or modification operations. It allocates a buffer to hold characters, which can be resized as needed, reducing the overhead of creating new strings with each modification.

3. **Append and Insert**: `StringBuilder` provides methods like `append` and `insert` that allow you to add characters, strings, or other data types to the sequence. These methods are efficient and can be chained together to build complex strings.

4. **String Conversion**: You can easily convert a `StringBuilder` object back to a `String` using the `toString()` method. This is useful when you need to obtain the final result.

Here's an example of how to use `StringBuilder` to concatenate strings efficiently:
*/

StringBuilder sb = new StringBuilder();

// Append strings to the StringBuilder
sb.append("Hello, ");
sb.append("world!");
sb.append(" This is a StringBuilder.");

// Convert StringBuilder to a String
String result = sb.toString();

System.out.println(result); // Output: Hello, world! This is a StringBuilder.
/*
Using `StringBuilder` can lead to better performance and reduced memory overhead compared to repeatedly concatenating strings using the `+` operator or `concat` method, especially when dealing with large or frequent string manipulations.
*/
```
### Python
``` python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        len1, len2 = len(num1), len(num2)
        result = [0] * (len1 + len2)

        for i in range(len1 - 1, -1, -1):
            for j in range(len2 - 1, -1, -1):
                digit1, digit2 = ord(num1[i]) - ord('0'), ord(num2[j]) - ord('0')
                product = digit1 * digit2
                total = product + result[i + j + 1]
                result[i + j + 1] = total % 10
                result[i + j] += total // 10

        result_str = ''.join(map(str, result)).lstrip('0')
        return result_str if result_str else '0'
```
### JavaScript
``` javascript
var multiply = function(num1, num2) {
    const len1 = num1.length;
    const len2 = num2.length;
    const result = new Array(len1 + len2).fill(0);

    for (let i = len1 - 1; i >= 0; i--) {
        for (let j = len2 - 1; j >= 0; j--) {
            const digit1 = num1.charCodeAt(i) - '0'.charCodeAt(0);
            const digit2 = num2.charCodeAt(j) - '0'.charCodeAt(0);
            const product = digit1 * digit2;
            const total = product + result[i + j + 1];
            result[i + j + 1] = total % 10;
            result[i + j] += Math.floor(total / 10);
        }
    }

    const resultStr = result.join('').replace(/^0+/, '');
    return resultStr || '0';
};
```
### Lua
``` lua
function multiply(num1, num2)
    local len1 = #num1
    local len2 = #num2
    local result = {}
    for i = 1, len1 + len2 do
        result[i] = 0
    end

    for i = len1, 1, -1 do
        for j = len2, 1, -1 do
            local digit1 = tonumber(num1:sub(i, i))
            local digit2 = tonumber(num2:sub(j, j))
            local product = digit1 * digit2
            local total = product + result[i + j + 1]
            result[i + j + 1] = total % 10
            result[i + j] = result[i + j] + math.floor(total / 10)
        end
    end

    local resultStr = table.concat(result)
    return resultStr:match('^0*') == resultStr and '0' or resultStr
end
```
### C++
``` c++
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    string multiply(string num1, string num2) {
        int len1 = num1.length();
        int len2 = num2.length();
        vector<int> result(len1 + len2, 0);

        for (int i = len1 - 1; i >= 0; i--) {
            for (int j = len2 - 1; j >= 0; j--) {
                int digit1 = num1[i] - '0';
                int digit2 = num2[j] - '0';
                int product = digit1 * digit2;
                int total = product + result[i + j + 1];
                result[i + j + 1] = total % 10;
                result[i + j] += total / 10;
            }
        }

        string resultStr;
        for (int digit : result) {
            resultStr += to_string(digit);
        }

        size_t start = resultStr.find_first_not_of('0');
        if (start != string::npos) {
            return resultStr.substr(start);
        } else {
            return "0";
        }
    }
};
```
### C
``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* multiply(char* num1, char* num2) {
    int len1 = strlen(num1);
    int len2 = strlen(num2);
    int* result = (int*)calloc(len1 + len2, sizeof(int));

    for (int i = len1 - 1; i >= 0; i--) {
        for (int j = len2 - 1; j >= 0; j--) {
            int digit1 = num1[i] - '0';
            int digit2 = num2[j] - '0';
            int product = digit1 * digit2;
            int total = product + result[i + j + 1];
            result[i + j + 1] = total % 10;
            result[i + j] += total / 10;
        }
    }

    int start = 0;
    while (start < len1 + len2 - 1 && result[start] == 0) {
        start++;
    }

    char* resultStr = (char*)malloc((len1 + len2 - start + 1) * sizeof(char));
    int index = 0;
    for (int i = start; i < len1 + len2; i++) {
        resultStr[index++]
```
