# [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/9bcf4f65-a42c-4b8b-8dfa-b0b05980df73)
## Solution
##### (986/987 test cases are successfully executed. 1 test case fails because the text is very long, thus memory limit exceeds)
``` java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int length = s.length();

        // if the length of the given string is 0 or 1
        if (length == 1) {
            return 1;
        } else if (length == 0) {
            return 0;
        }

        // To store all the substrings
        String strs[] = new String[(length * length)];

        // Initialized all the strings to "" as there is a requirement
        // for calculation of length on line number and length of null strings cannot be calculated
        for (int i = 0; i < (length * length); i++) {
            strs[i] = "";
        }


        int k = 0;
        String str = "";
        String nextC;
        for (int j = 0; j < length; j++) {
            for (int i = j; i < length; i++) {

            // A character cannot ba converted to string directly
            // So adding a string to a character the result becomes a string.
            nextC = "" + s.charAt(i);

            // the contains() check for the presence of a sequence of characters in the string
            if (!str.contains(nextC)) {
                str = str + nextC;
            } else {
                strs[k] = str;
                k++;

                // if the consecutive characters are not same
                if (!nextC.contains("" + s.charAt(i - 1))) {
                    str = s.charAt(i - 1) + nextC;
                } else {
                    str = nextC;
                }
                // str = nextC;
            }

            // For the last substring 
            // for example "kew" in pwwkew
            strs[k] = str;
            k++;
            }

            // Emptied the str for next iteration
            str = "";
        }
        

        int maxLength = 0;
        int strLength;
        for (int i = 0; i < (length * length); i++) {
            // if (strs[i].equals("")) {
            //     break;
            // }
            strLength = strs[i].length();
            if (strLength > maxLength) {
                maxLength = strLength;
            }
        }
        return maxLength;
    }
}
```

#### I will solve this problem using python and also update in java version
