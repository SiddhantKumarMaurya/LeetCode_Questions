# [Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/description/?envType=daily-question&envId=2024-04-04)
## Topics: `String`, `Stack`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/01cbaa14-6c91-4039-ab53-6c3549235311)
## Solution (By using Stack)
```java
import java.util.Stack;
class Solution {
    public int maxDepth(String s) {
        Stack<Character> stack = new Stack<>();
        int maxDepth = 0;
        int currentDepth = 0;
        int length = s.length();
        for (int i = 0; i < length; i++) {
            char c = s.charAt(i);
            if (c == '(') {
                stack.push(c);
                currentDepth++;
            } else if(c == ')') {
                if (stack.peek() == '(') {
                    stack.pop();
                    maxDepth = Math.max(maxDepth, currentDepth);
                    currentDepth--;
                }
            }
        }
        return maxDepth;
    }
}
```
---
## Solution
```java
class Solution {
    public int maxDepth(String s) {
        int maxDepth = 0;
        int currentDepth = 0;
        
        for (char c : s.toCharArray()) {
            if (c == '(') {
                currentDepth++;
                maxDepth = Math.max(maxDepth, currentDepth);
            } else if (c == ')') {
                currentDepth--;
            }
        }
        
        return maxDepth;
    }
}
```
