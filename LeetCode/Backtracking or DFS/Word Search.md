# [Word Search](https://leetcode.com/problems/word-search/?envType=daily-question&envId=2024-04-03)
## Topics: `Array`, `String`, `Backtracking`, `Matrix`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/76a0fef4-aec0-43fd-a738-b98458089c3b)
## Solution (Incorrect)
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;
        int startRow = 0;
        int startColumn = 0;
        boolean[][] searched = new boolean[m][n];

        for (int i = 0; i < m; i++) {
            Arrays.fill(searched[i], false);
        }

        int charIndex = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                char letter = word.charAt(charIndex);
                if (letter == board[i][j]) {
                    startRow = i;
                    startColumn = j;
                    searched[i][j] = true;
                    charIndex++;
                } else return false;
            }
        }
        int i = startRow;
        int j = startColumn;
        while (charIndex != word.length()) {
            char letter = word.charAt(charIndex);
            if (!searched[i + 1][j]) {
                if (letter == board[i + 1][j]) {
                    searched[i + 1][j] = true;
                    charIndex++;
                    i = i + 1;
                }
            } else if(!searched[i - 1][j]) {
                if (letter == board[i - 1][j]) {
                    searched[i - 1][j] = true;
                    charIndex++;
                    i = i - 1;
                }
            } else if(!searched[i][j + 1]) {
                if (letter == board[i][j + 1]) {
                    searched[i][j + 1] = true;
                    charIndex++;
                    j = j + 1;
                }
            } else if(!searched[i][j - 1]) {
                if (letter == board[i][j - 1]) {
                    searched[i][j - 1] = true;
                    charIndex++;
                    j = j - 1;
                }
            } else return false;
        }
        if (charIndex == word.length()) return true;
        else return false;
    }
}
```
---
## Solution
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;
        
        // Iterate through each cell in the board
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (search(board, word, i, j, 0)) { // If word found starting from current cell, return true
                    return true;
                }
            }
        }
        return false; // If word not found anywhere in the board
    }
    
    // Recursive function to search for the word starting from a given cell
    private boolean search(char[][] board, String word, int i, int j, int index) {
        // Base case: If all characters of the word have been found
        if (index == word.length()) {
            return true;
        }
        
        // Boundary conditions and character match check
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(index)) {
            return false;
        }
        
        // Mark the current cell as visited
        char temp = board[i][j];
        board[i][j] = '#';
        
        // Search in all four directions recursively
        boolean found = search(board, word, i + 1, j, index + 1) || // Down
                        search(board, word, i - 1, j, index + 1) || // Up
                        search(board, word, i, j + 1, index + 1) || // Right
                        search(board, word, i, j - 1, index + 1);   // Left
        
        // Restore the original value of the current cell
        board[i][j] = temp;
        
        return found;
    }
}
```
---
`We can use search pruning to optimize the backtracking solution and make it faster, especially for larger boards. Search pruning involves intelligently skipping unnecessary branches of the search tree to reduce the number of recursive calls and improve performance.

Here are some techniques we can use for search pruning in the word search problem:

1. Early Termination: If we find a match for the word while exploring a path, we can immediately terminate the search and return true, as we've already found the word.

2. Heuristic Ordering: We can prioritize exploring paths that are more likely to lead to a match for the word. For example, we can start the search from cells that are more likely to contain the first character of the word.

3. Backtracking Optimization: We can optimize the backtracking process by avoiding unnecessary recursion and duplicate work. For example, we can prune branches of the search tree if we know that they cannot lead to a match for the word.

4. Memoization: We can use memoization to store the results of previous searches for specific cell positions and word indices. This allows us to avoid redundant computations by reusing previously computed results.

By implementing these search pruning techniques, we can significantly improve the efficiency of the backtracking solution and make it faster, especially for larger boards and longer words. However, it's important to balance the complexity of the optimization techniques with the potential performance gains and maintainability of the code.
`
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;
        
        // Iterate through each cell in the board
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (search(board, word, i, j, 0, new boolean[m][n])) { // If word found starting from current cell, return true
                    return true;
                }
            }
        }
        return false; // If word not found anywhere in the board
    }
    
    // Recursive backtracking function with search pruning
    private boolean search(char[][] board, String word, int i, int j, int index, boolean[][] visited) {
        // Base case: If all characters of the word have been found
        if (index == word.length()) {
            return true;
        }
        
        // Boundary conditions and character match check
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || visited[i][j] || board[i][j] != word.charAt(index)) {
            return false;
        }
        
        // Mark the current cell as visited
        visited[i][j] = true;
        
        // Search in all four directions recursively
        boolean found = search(board, word, i + 1, j, index + 1, visited) || // Down
                        search(board, word, i - 1, j, index + 1, visited) || // Up
                        search(board, word, i, j + 1, index + 1, visited) || // Right
                        search(board, word, i, j - 1, index + 1, visited);   // Left
        
        // Unmark the current cell before backtracking
        visited[i][j] = false;
        
        return found;
    }
}
```
