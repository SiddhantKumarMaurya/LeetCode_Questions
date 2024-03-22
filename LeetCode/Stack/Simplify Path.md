# [Simplify Path](https://leetcode.com/problems/simplify-path/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/82265848-f8e4-4348-ab56-32dd5527b7ec)
## Solution
```java
import java.util.Stack;
// import java.lang.StringBuilder; // imported automatically, no need for manual import
// since all the classes, intefaces of java.lang package are automatically imported
class Solution {
    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<>();
        String[] parts = path.split("/");

        for (String part: parts) {
            // Ignore current directory and empty parts
            if (part.equals(".") || part.equals("")) {
                continue;
            } else if (part.equals("..")) {
                if (!stack.isEmpty()) {
                    stack.pop(); // Go one level up
                }
            } else {
                stack.push(part); // push the directory onto the stack
            }
        }

        StringBuilder result = new StringBuilder("/");
        for (String dir: stack) {
            result.append(dir).append("/");
        }

        // Removes trailing slashes
        if (result.length() > 1) {
            result.setLength(result.length() - 1);
        }

        return result.toString();
    }
}
```
## Solution
```java
import java.util.Stack;
import java.util.StringTokenizer;

public class Solution {
    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<>();
        StringTokenizer tokenizer = new StringTokenizer(path, "/");

        while (tokenizer.hasMoreTokens()) {
            String token = tokenizer.nextToken();

            if (token.equals("..")) {
                if (!stack.isEmpty()) {
                    stack.pop();
                }
            } else if (!token.equals(".") && !token.isEmpty()) {
                stack.push(token);
            }
        }

        StringBuilder result = new StringBuilder();
        for (String dir : stack) {
            result.append("/");
            result.append(dir);
        }

        return result.length() > 0 ? result.toString() : "/";
    }
}
```
