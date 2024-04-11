# [Remove K Digits](https://leetcode.com/problems/remove-k-digits/description/?envType=daily-question&envId=2024-04-11)
## Topics: `String`, `Stack`, `Greedy`, `Monotonic Stack`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ca14b9fd-ea02-479d-8acb-82c4fb31141b)
## Solution (Incorect)
```java
import java.util.Stack;
class Solution {
    public String removeKdigits(String num, int k) {
        int length = num.length();
        if (length == k) return "0";
        int range = (int)(Math.pow(10, length - k));
        String str = "";
        for (int i = 0; i < range; i++) {
            str = "" + i;
            int l = str.length();
            int j = 0;
            int previousIndex = num.indexOf(str.charAt(j));
            if (previousIndex == -1) continue;
            j++;
            while (j < l){
                // we can also use str.Contains(Character.toString(ch)) to find if ch is present in str.
                int currentIndex = num.indexOf(str.charAt(j));
                // this logic is flawed, as if there are two same numbers that appear consecutively, indexOf() return only the index of first presence of the number.
                if (currentIndex == -1 || currentIndex == previousIndex || previousIndex > currentIndex) break;
                j++;
            }
            if (j == l && str.length() == length - k) break;
        }
        return str;
    }
}
```
---
## Solution (Monotonic Stack)
```java
import java.util.Stack;

class Solution {
    public String removeKdigits(String num, int k) {

        if (num.length() == k) return "0";
        
        Stack<Character> stack = new Stack<>();
        
        for (char digit : num.toCharArray()) {
            while (!stack.isEmpty() && k > 0 && stack.peek() > digit) {
                stack.pop();
                k--;
            }
            stack.push(digit);
        }
        
        // If there are still remaining removals (k > 0), remove digits from the end of the stack
        while (k > 0 && !stack.isEmpty()) {
            stack.pop();
            k--;
        }
        
        // Construct the smallest possible number from the remaining digits in the stack
        StringBuilder result = new StringBuilder();
        while (!stack.isEmpty()) {
            result.insert(0, stack.pop());
        }
        // if we do result.append(stack.pop()) and result.reverse(), it takes less time for execution.
        
        // Remove leading zeroes
        while (result.length() > 1 && result.charAt(0) == '0') {
            result.deleteCharAt(0);
        }
        
        // If the result is empty, return "0"
        if (result.length() == 0) {
            return "0";
        }
        
        return result.toString();
    }
}
```
---
## Solution (Greedy Approach)
```java
class Solution {
    public String removeKdigits(String num, int k) {
        int n = num.length();
        if (n == k) return "0"; // If we need to remove all digits, the result is "0".

        StringBuilder sb = new StringBuilder();
        int removedDigits = 0; // Counter for removed digits

        for (char digit : num.toCharArray()) {
            while (removedDigits < k && sb.length() > 0 && sb.charAt(sb.length() - 1) > digit) {
                sb.deleteCharAt(sb.length() - 1); // Remove digits that make the number larger
                removedDigits++;
            }
            sb.append(digit); // Append the current digit
        }

        // Remove remaining digits from the end if needed
        while (removedDigits < k) {
            sb.deleteCharAt(sb.length() - 1);
            removedDigits++;
        }

        // Remove leading zeros
        int leadingZeroIndex = 0;
        while (leadingZeroIndex < sb.length() && sb.charAt(leadingZeroIndex) == '0') {
            leadingZeroIndex++;
        }

        sb.delete(0, leadingZeroIndex);

        // If the resulting string is empty, return "0"
        if (sb.length() == 0) {
            return "0";
        }

        return sb.toString();
    }
}
```
