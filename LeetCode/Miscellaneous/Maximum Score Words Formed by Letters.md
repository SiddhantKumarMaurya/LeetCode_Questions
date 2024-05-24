# [Maximum Score Words Formed by Letters](https://leetcode.com/problems/maximum-score-words-formed-by-letters/description/)
## Topics: `Array`, `String`, Dynamic Programming, `Backtracking`, `Bit Manipulation`, `Bitmask`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/719d7519-4407-470a-839f-627f3387b654)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/e6f4fc01-1357-44cb-9db2-3283bd9d7192)
## Solution
```c++
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Solution {
    public int maxScoreWords(String[] words, char[] letters, int[] score) {
        int[] letterCount = new int[26];
        for (char c : letters) {
            letterCount[c - 'a']++;
        }
        return backtrack(words, letterCount, score, 0);
    }

    private int backtrack(String[] words, int[] letterCount, int[] score, int index) {
        if (index == words.length) {
            return 0;
        }

        // Skip the current word
        int maxScore = backtrack(words, letterCount, score, index + 1);

        // Try to include the current word
        String word = words[index];
        int[] countCopy = letterCount.clone();
        boolean canFormWord = true;
        int wordScore = 0;

        for (char c : word.toCharArray()) {
            if (countCopy[c - 'a']-- <= 0) {
                canFormWord = false;
            }
            wordScore += score[c - 'a'];
        }

        if (canFormWord) {
            maxScore = Math.max(maxScore, wordScore + backtrack(words, countCopy, score, index + 1));
        }

        return maxScore;
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        String[] words1 = {"dog", "cat", "dad", "good"};
        char[] letters1 = {'a', 'a', 'c', 'd', 'd', 'd', 'g', 'o', 'o'};
        int[] score1 = {1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
        System.out.println(sol.maxScoreWords(words1, letters1, score1)); // Output: 23

        String[] words2 = {"xxxz", "ax", "bx", "cx"};
        char[] letters2 = {'z', 'a', 'b', 'c', 'x', 'x', 'x'};
        int[] score2 = {4, 4, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 5, 0, 10};
        System.out.println(sol.maxScoreWords(words2, letters2, score2)); // Output: 27

        String[] words3 = {"leetcode"};
        char[] letters3 = {'l', 'e', 't', 'c', 'o', 'd'};
        int[] score3 = {0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0};
        System.out.println(sol.maxScoreWords(words3, letters3, score3)); // Output: 0
    }
}
```
