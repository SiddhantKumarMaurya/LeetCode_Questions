# [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Two Pointers`, `String`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/aa2d0985-a7a7-47c7-bc79-1c4df1f6784f)
## Solution (Initial Thought) (I will work; I need to refer it)
```java
import java.util.Collections;
import java.util.ArrayList;
import java.util.Arrays;
class Solution {
    public String reverseWords(String s) {
        // split() method takes regular expression as input
        String[] stringArray = s.split(" "); // We don't need to use any wrapper class as String itself is a class.
        // cannot directly pass array
        // StringBuilder str = new StringBuilder(stringArray);

        // ArrayList<String> list = Arrays.asList(stringArray); // somehow this did not work
        ArrayList<String> list = new ArrayList<>(Arrays.asList(stringArray));
        Collections.reverse(list);
        stringArray = list.toArray(new String[0]); // if we don't specify the type it will create an array of type Object;


        StringBuilder str = new StringBuilder();
        int length = stringArray.length;
        

        for (int i = 0; i < length; i++) {
            str.append(stringArray[i]);
            if (i != length - 1) {
                str.append(" ");
            }
        }
        return str.toString();
    }
}
```
## Solution (Very Slow; need to find a faster solution)
```java
class Solution {
    public String reverseWords(String s) {
        int length = s.length();
        String tempStr = "";
        StringBuilder str = new StringBuilder();
        for (int i = length - 1; i >= 0; i--) {
            char letter = s.charAt(i);
            if (letter != ' ') {
                tempStr = letter + tempStr;
            } else {
                str.append(tempStr);
                tempStr = "";
                if (i != 0 && str.length() > 0 && (str.charAt(str.length() - 1) != ' ')) {
                    str.append(" ");
                }
            }
        }
        return str.append(tempStr).toString().trim();
    }
}
```
