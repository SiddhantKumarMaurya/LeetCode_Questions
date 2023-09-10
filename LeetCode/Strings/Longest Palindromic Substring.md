# [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/7f8f4bf1-9563-40f1-b2d7-393f4868c929)
## Solution (First)
##### All the test cases pass but the time limit exceeds as the complexity of this program is O(n<sup>3</sup>).
``` java
class Solution {

    public static boolean isPalindrome(String str) {
        int left = 0, right = str.length() - 1;
        
        while(left < right)
        {
            if(str.charAt(left) != str.charAt(right))
            {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }

    public String longestPalindrome(String s) {
        
        String c = "";
        String str = "";
        int length = s.length();
        int longest = 0;
        String lngstPalinStr = "";

        for (int i = 0; i < length; i++) {
            for (int j = i; j < length; j++) {
                c = "" + s.charAt(j);
                str = str + c;
                if (isPalindrome(str)) {
                    if (longest < str.length()) {
                        longest = str.length();
                        lngstPalinStr = str;
                    }
                }
            }
            str = "";
        }

        return lngstPalinStr;
    }
}
```
## Solution (Second)
##### All the test cases pass and is successfully accepted but it's time complexity is O(n<sup>2</sup>). So, learn about manacher's algorithm. Manacher's Algorithm is an algorithm to find Longest Palindromic Substring in a string and its time complexity is O(n)
``` java
// Dynamic Programming Method

class Solution {
    public String longestPalindrome(String s) {
    if(s==null || s.length()<=1)
        return s;
 
    int len = s.length();
    int maxLen = 0;

    // Make a matrix:
    // dp[i][j] = true, if it is the center of palindrome string
    boolean [][] dp = new boolean[len][len];
 
    String longest = null;
    for(int p=0; p<s.length(); p++){
        // i<len-p, to ensure that
        for(int i=0; i<len - p; i++){
            int j = i+p;

            // At first all the diagonals are marked as they are the centres of all palindromes
            // then all the adjacent letter (such as a, a in cabac) which are same are marked 
            // by (j-i<=2) condition
            // finally, all letters at 3rd, 4th, 5th and so on,(c,c in cabac) positions on left 
            // and right side 
            // of palindrome center are marked by dp[i+1][j-1]
                if(s.charAt(i)==s.charAt(j) && (j-i<=2||dp[i+1][j-1])){
                    dp[i][j]=true;

                    if(j-i+1>maxLen){
                    maxLen = j-i+1; 
                    longest = s.substring(i, j+1);
                    }
                }
        }
 
    }
    return longest;
    }
}


/*  d a b c b a
d 1       
a   1       1
b     1   1  
c       1    
b         1  
a           1
*/
```
