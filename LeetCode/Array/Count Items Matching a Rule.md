# [Count Items Matching a Rule](https://leetcode.com/problems/count-items-matching-a-rule/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/3bbe1f4b-636b-4d21-8fd1-507100233e9b)
## Solution
```java
class Solution {
    public int countMatches(List<List<String>> items, String ruleKey, String ruleValue) {

        // Get the size of list
        int length = items.size();

        // To store the number of matching cases
        int count = 0;

        // To access the list within the list
        int j = 0;

        // Iterate through the list
        for (int i = 0; i < length; i++) {

            // To set the indexes of "type" as 0
            if (ruleKey.equals("type")) {
                j = 0;
            }

            // To set the index of "color" as 1
            else if (ruleKey.equals("color")) {
                j = 1;
            }

            // To set the index of "name" as 2
            else j = 2;

            // Check for matches
            if (items.get(i).get(j).equals(ruleValue)) {

                // Increment if match is found
                count++;
            }
        }
        return count;
    }
}
```
