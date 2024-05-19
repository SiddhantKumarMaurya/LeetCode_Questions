# [Generate Parantheses](https://leetcode.com/problems/generate-parentheses/submissions/1233891250/)
## Topics: `String`, `Dynamic Programming`, `Backtracking`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/89929238-9674-48d9-8054-e3dbf74b0916)
## Solution
```java
import java.util.List;
import java.util.Stack;
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        Stack<State> stack = new Stack<>();
        stack.push(new State("", 0, 0));
        while (!stack.isEmpty()) {
            State currentState = stack.pop();
            if (currentState.openCount == n && currentState.closeCount == n) {
                list.add(currentState.currentString);
            }

            if (currentState.openCount < n) {
                stack.push(new State(currentState.currentString + "(", currentState.openCount + 1, currentState.closeCount));
            }
            if (currentState.closeCount < currentState.openCount) {
                stack.push(new State(currentState.currentString + ")", currentState.openCount, currentState.closeCount + 1));
            }
        }
        return list;
    }

    private static class State {
        String currentString;
        int openCount;
        int closeCount;
        State(String currentString, int openCount, int closeCount) {
            this.currentString = currentString;
            this.openCount = openCount;
            this.closeCount = closeCount;
        }
    }
}
```
