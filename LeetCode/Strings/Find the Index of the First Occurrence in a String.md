# [Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/753ac8a3-eb45-42fb-a3f9-f340c41cc09b)
## Solution (Java)
``` java
class Solution {
    public int strStr(String haystack, String needle) {
     int needleLength = needle.length();
     int haystackLength = haystack.length();
     String potentialNeedle;

     for (int i = 0; i < haystackLength; i++) {
         int beg = i;
         int end = i + needleLength;

         // max value of end should be equal to the length of string
         // (this will help int substring function)
         if (end <= haystackLength) {
             potentialNeedle = haystack.substring(beg, end);
             if (potentialNeedle.equals(needle)) {
                 return i;
             }
         } else {
             break;
         }
     }
     return -1;
    }
}
```
## Solution (Python)
``` Python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        needleLength = len(needle)
        haystackLength = len(haystack)

        for i in range(haystackLength):
            beg = i
            end = i + needleLength

            # Ensure that end does not exceed the length of the string
            if end <= haystackLength:
                potentialNeedle = haystack[beg:end]
                if potentialNeedle == needle:
                    return i
            else:
                break

        return -1
```
## Solution (JavaScript)
``` JavaScript
var strStr = function (haystack, needle) {
    const needleLength = needle.length;
    const haystackLength = haystack.length;

    for (let i = 0; i < haystackLength; i++) {
        const beg = i;
        const end = i + needleLength;

        // Ensure that end does not exceed the length of the string
        if (end <= haystackLength) {
            const potentialNeedle = haystack.substring(beg, end);
            if (potentialNeedle === needle) {
                return i;
            }
        } else {
            break;
        }
    }

    return -1;
};
```

## Solution (Lua)
``` Lua
function strStr(haystack, needle)
    local needleLength = string.len(needle)
    local haystackLength = string.len(haystack)

    for i = 1, haystackLength do
        local beg = i
        local endPos = i + needleLength

        -- Ensure that end does not exceed the length of the string
        if endPos <= haystackLength then
            local potentialNeedle = string.sub(haystack, beg, endPos)
            if potentialNeedle == needle then
                return i - 1 -- Lua uses 1-based indexing, so we subtract 1
            end
        else
            break
        end
    end

    return -1
end
```

## Solution (C++)
``` C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int needleLength = needle.length();
        int haystackLength = haystack.length();

        for (int i = 0; i < haystackLength; i++) {
            int beg = i;
            int endPos = i + needleLength;

            // Ensure that endPos does not exceed the length of the string
            if (endPos <= haystackLength) {
                string potentialNeedle = haystack.substr(beg, needleLength);
                if (potentialNeedle == needle) {
                    return i;
                }
            } else {
                break;
            }
        }

        return -1;
    }
};
```

### Solution (C)
``` C
#include <stdio.h>
#include <string.h>

int strStr(char *haystack, char *needle) {
    int needleLength = strlen(needle);
    int haystackLength = strlen(haystack);

    for (int i = 0; i < haystackLength; i++) {
        int beg = i;
        int endPos = i + needleLength;

        // Ensure that endPos does not exceed the length of the string
        if (endPos <= haystackLength) {
            char potentialNeedle[needleLength + 1];
            strncpy(potentialNeedle, haystack + beg, needleLength);
            potentialNeedle[needleLength] = '\0';

            if (strcmp(potentialNeedle, needle) == 0) {
                return i;
            }
        } else {
            break;
        }
    }

    return -1;
}

int main() {
    char haystack[] = "hello";
    char needle[] = "ll";
    int result = strStr(haystack, needle);
    printf("%d\n", result);
    return 0;
}
```
