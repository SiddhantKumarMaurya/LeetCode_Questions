# [Basic Calculator](https://leetcode.com/problems/basic-calculator/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Math`, `String`, `Stack`, `Recursion`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/fd5dcccd-cf50-4b5f-9853-4ef4005fdce1)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/51b1c669-eb1c-477f-85f1-a8d29cac6caf)
## Solution (Incorrect)
```java
class Solution {
    public int calculate(String s) {
        Stack<Character> stack = new Stack<>();
        int length = s.length();
        StringBuilder sb = new StringBuilder("(" + s.replaceAll("\\s", "") + ")");
        // we can also write replaceAll(" ", "") which only remove spaces not tabs and newlines.
        sb.reverse();
        StringBuilder newStr = new StringBuilder();

        for (int i = 0; i < length; i++) {
            char c = sb.charAt(i);
            if (c == ')' || c == '+' || c == '-') {
                stack.push(c);
            } else if (c == '(') {
                char stackElement = stack.pop();
                while (!stack.isEmpty() || stackElement != ')') {
                    newStr.append(stackElement);
                    stackElement = stack.pop();
                }
            } else {
                newStr.append(c);
            }
        }
        return Integer.parseInt(calculateHelper(newStr.reverse().toString()));
    }

    public String calculateHelper(String str) {
        if (str.charAt(0) == '+' || str.charAt(0) == '-') {
            String s = calculateHelper(str.substring(1));
            if (str.charAt(0) == '+') {
                // Error: Index 2 out of bounds for length 2.
               int eval = (int)s.charAt(1) + (int)s.charAt(2);
               return eval + str.substring(3);
            } else if (str.charAt(0) == '-') {
                int eval = (int)str.charAt(1) - (int)str.charAt(2);
                return eval + str.substring(3);
            }
        }
        return str;
    }
}
```
---
## Solution (Correct)
```java
import java.util.Stack;

class Solution {
    public int calculate(String s) {
        Stack<Integer> stack = new Stack<>();
        int num = 0;
        int result = 0;
        int sign = 1; // 1 for positive, -1 for negative

        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                num = num * 10 + (c - '0');
            } else if (c == '+') {
                result += sign * num;
                num = 0;
                sign = 1;
            } else if (c == '-') {
                result += sign * num;
                num = 0;
                sign = -1;
            } else if (c == '(') {
                stack.push(result);
                stack.push(sign);
                result = 0;
                sign = 1;
            } else if (c == ')') {
                result += sign * num;
                num = 0;
                result *= stack.pop(); // pop the sign before the parenthesis
                result += stack.pop(); // add the result before the parenthesis
            }
        }

        if (num != 0) {
            result += sign * num;
        }

        return result;
    }
}
```
