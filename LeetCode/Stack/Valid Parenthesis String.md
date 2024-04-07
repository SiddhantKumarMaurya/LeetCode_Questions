# [Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/description/?envType=daily-question&envId=2024-04-07)
## Topics:`String`, `Dynamic Programming`, `Stack`, `Greedy`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b95d4d88-439a-4d2c-af4e-4da952274582)
## Solution (Initial Thought) (Incorrect)
```java
class Solution {
    public boolean checkValidString(String s) {
        int length = s.length();
        int leftParantheses = 0;

        for (int i = 0; i < length; i++) {
            if (s.charAt(i) == '(') {
                leftParantheses++;
            } else if (s.charAt(i) == '*') {
                leftParantheses++;
            } else leftParantheses--;
        }

        int rightParantheses = 0;
        for (int i = length - 1; i >= 0; i--) {
            if (s.charAt(i) == ')') {
                rightParantheses++;
            } else if (s.charAt(i) == '*') {
                rightParantheses++;
            } else rightParantheses--;
        }

        if (leftParantheses == 0 || rightParantheses == 0 || rightParantheses == leftParantheses) return true;
        return false;
    }
}
```
---
## Solution (Initial Thought) (Incorrect)
```java
class Solution {
    public boolean checkValidString(String s) {
        int length = s.length();
        int leftParantheses = 0;
        int rightParantheses = 0;
        int astrisks = 0;

        for (int i = 0; i < length; i++) {
            if (s.charAt(i) == '(') leftParantheses ++;
            else if (s.charAt(i) == '*') astrisks ++;
            else rightParantheses ++;
        }

        // we need to subtract astrisks only if leftParantheses != rightParantheses
        return (Math.abs(leftParantheses - rightParantheses) - astrisks) <= 0;
    }
}
```
---
## Solution (Stack Implementation)
```java
import java.util.Stack;

class Solution {
    public boolean checkValidString(String s) {
        Stack<Integer> leftParenStack = new Stack<>();
        Stack<Integer> asteriskStack = new Stack<>();
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(') {
                leftParenStack.push(i);
            } else if (c == '*') {
                asteriskStack.push(i);
            } else {
                if (!leftParenStack.isEmpty()) {
                    leftParenStack.pop();
                } else if (!asteriskStack.isEmpty()) {
                    asteriskStack.pop();
                } else {
                    return false;
                }
            }
        }
        
        while (!leftParenStack.isEmpty() && !asteriskStack.isEmpty()) {
            if (leftParenStack.pop() > asteriskStack.pop()) {
                return false;
            }
        }
        
        return leftParenStack.isEmpty();
    }
}
```
---
## Solution (Another Approach)
```java
class Solution 
{
   public boolean checkValidString(String s) 
   {
     int low=0,high=0;
     for(int i=0;i<s.length();i++)
     {
        if(s.charAt(i)=='(')
        {
          low++;
          high++;
        }
        else if(s.charAt(i)==')')
        {
          low=Math.max(0,--low);
          high--;
        }
        else 
        {
          low=Math.max(0,--low);
          high++;
        } 
        if(high<0)
        return false;   
     }
     return (low==0);
   }
}
```
