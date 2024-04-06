# [Make the String Great](https://leetcode.com/problems/make-the-string-great/description/?envType=daily-question&envId=2024-04-05)
## Topics: `String`, `Stack`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/30831efd-da16-4535-90e4-87a2b0b42253)
## Solution 
```java
import java.util.Stack;
import java.util.EmptyStackException;
class Solution {
    public String makeGood(String s) {
        StringBuilder sb = new StringBuilder();
        Stack<Character> stack = new Stack<>();
        int length = s.length();
        for (int i = 0; i < length; i++) {
            try {
                if(Character.isUpperCase(s.charAt(i))) {
                    if (stack.peek() == Character.toLowerCase(s.charAt(i))) {
                        stack.pop();
                        continue;
                    }
                }else if(Character.isLowerCase(s.charAt(i))) {
                    if (stack.peek() == Character.toUpperCase(s.charAt(i))) {
                        stack.pop();
                        continue;
                    }
                }
            } catch (EmptyStackException e) {
                stack.push(s.charAt(i));
                continue;
            }
            stack.push(s.charAt(i));
        }

        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }

        return sb.reverse().toString();
    }
}
```
---
## Solution
```java
class Solution {
    public String makeGood(String s) {
        StringBuilder sb = new StringBuilder();
        int length = s.length();

        for (int i = 0; i < length; i++) {
            char currentChar = s.charAt(i);
            if (!sb.isEmpty()) {
                int sbLength = sb.length();
                char sbLastChar = sb.charAt(sbLength - 1);
                if (Math.abs(currentChar - sbLastChar) == 32) {
                    sb.delete(sbLength - 1, sbLength);
                    // or we can do
                    // sb.deleteCharAt(sbLength - 1)
                } else {
                    sb.append(currentChar);
                }
            } else {
                sb.append(currentChar);
            }
        }
        return sb.toString();
    }
}
```
