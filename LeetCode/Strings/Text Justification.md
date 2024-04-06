# [Text Justification](https://leetcode.com/problems/text-justification/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `String`, `Simulation`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/3a111171-0e80-4ef9-8c3b-d341ee678fe7)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d2dbfe10-c7cf-4b39-a20e-e51f86b249bf)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/5ec9c77e-4ac4-4d00-9b74-6359a9ed0c8b)
## Solution
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> result = new ArrayList<>();
        int index = 0;
        while (index < words.length) {
            int lineLength = words[index].length();
            int endIndex = index + 1;
            while (endIndex < words.length && lineLength + words[endIndex].length() + 1 <= maxWidth) {
                lineLength += words[endIndex].length() + 1;
                endIndex++;
            }
            StringBuilder sb = new StringBuilder();
            int numOfWords = endIndex - index;
            int numOfSpaces = maxWidth - lineLength + numOfWords - 1;
            if (numOfWords == 1 || endIndex == words.length) {
                // Left justify the last line or a line with only one word
                for (int i = index; i < endIndex; i++) {
                    sb.append(words[i]);
                    if (i < endIndex - 1) sb.append(" ");
                }
                for (int i = sb.length(); i < maxWidth; i++) {
                    sb.append(" ");
                }
            } else {
                int avgSpaces = numOfSpaces / (numOfWords - 1);
                int extraSpaces = numOfSpaces % (numOfWords - 1);
                for (int i = index; i < endIndex; i++) {
                    sb.append(words[i]);
                    if (i < endIndex - 1) {
                        for (int j = 0; j < avgSpaces; j++) sb.append(" ");
                        if (extraSpaces-- > 0) sb.append(" ");
                    }
                }
            }
            result.add(sb.toString());
            index = endIndex;
        }
        return result;
    }
}

```
