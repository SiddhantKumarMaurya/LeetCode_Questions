# [Length of Last Word](https://leetcode.com/problems/length-of-last-word/description/?envType=daily-question&envId=2024-04-01)
## Topics: `String`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d74a82ba-7091-449c-9a36-cb9aefecde49)
## Solution
```java
class Solution {
    public int lengthOfLastWord(String s) {
        String[] stringArray = s.split(" ");
        int length = stringArray.length;
        return stringArray[length -1].length();
    }
}
```
