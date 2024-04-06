# [Minumum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/description/?envType=daily-question&envId=2024-04-06)
## Topic: `String`, `Stack`
## Problem Statement:
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/250f4b54-096d-4cb9-9bee-b48c32d3ab90)
## Solution
```java
class Solution {
    public String minRemoveToMakeValid(String s) {
        int leftParanthesesCount = 0;
        int rightParanthesesCount = 0;

        StringBuilder sb = new StringBuilder(s);
        for (int i = 0; i < sb.length(); i++) {
            if (sb.charAt(i) == '(') {
                leftParanthesesCount ++;
            } else if (sb.charAt(i) == ')') {
                leftParanthesesCount --;
                if (leftParanthesesCount < 0) {
                    sb.deleteCharAt(i);
                    // We are decrementing the value of i here as we want to visit the same index as the string will be shifted.
                    i--;
                    leftParanthesesCount ++;
                }
            }
        }
        for (int i = sb.length() - 1; i >= 0; i--) {
            if (sb.charAt(i) == ')') {
                rightParanthesesCount ++;
            } else if (sb.charAt(i) == '(') {
                rightParanthesesCount --;
                if (rightParanthesesCount < 0) {
                    sb.deleteCharAt(i);
                    // we are not increasing i here because the string will be shifted to left and out counter i is also being shifted to left.
                    rightParanthesesCount ++;
                }
            }
        }
        return sb.toString();
    }
}
```
