# [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/description/)
## Topics: `Two Pointers`, `String`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/05688421-f384-48e0-aad8-06adb738ea69)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ac13bacd-5a72-4988-8fb6-d98bf4606855)
## Solution
```java
class Solution {
    public int compareVersion(String version1, String version2) {
        // split() take a regular expression so we can't use "."'
        String[] version1Revisions = version1.split("\\.");
        String[] version2Revisions = version2.split("\\.");
        return helper(0, version1Revisions, version2Revisions);
    }

    private int helper(int i, String[] version1Revisions, String[] version2Revisions) {
        int length1 = version1Revisions.length;
        int length2 = version2Revisions.length;

        if (i > length1 - 1 && i > length2 - 1) {
            return 0;
        } else if (i > length1 - 1) {
            if (Integer.parseInt(version2Revisions[i]) > 0) return -1;
            else return helper(i + 1, version1Revisions, version2Revisions);
        } else if (i > length2 - 1) {
            if (Integer.parseInt(version1Revisions[i]) > 0) return 1;
            else return helper(i + 1, version1Revisions, version2Revisions);
        } else if (Integer.parseInt(version1Revisions[i]) < Integer.parseInt(version2Revisions[i])) return -1;
        else if (Integer.parseInt(version1Revisions[i]) > Integer.parseInt(version2Revisions[i])) return 1;
        else return helper(i + 1, version1Revisions, version2Revisions);
    }
}
```
----
## Solution
```java
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] parts1 = version1.split("\\.");
        String[] parts2 = version2.split("\\.");
        
        int i = 0, j = 0;
        while (i < parts1.length || j < parts2.length) {
            int num1 = i < parts1.length ? Integer.parseInt(parts1[i]) : 0;
            int num2 = j < parts2.length ? Integer.parseInt(parts2[j]) : 0;
            
            if (num1 < num2) return -1;
            else if (num1 > num2) return 1;
            
            i++;
            j++;
        }
        
        return 0;
    }
}
```
