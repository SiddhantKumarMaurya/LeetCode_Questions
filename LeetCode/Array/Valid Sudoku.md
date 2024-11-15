# [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/?envType=study-plan-v2&envId=top-interview-150)
## Solution:
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        // Create hash sets for rows, columns, and sub-boxes
        HashSet<Character>[] rows = new HashSet[9];
        HashSet<Character>[] cols = new HashSet[9];
        HashSet<Character>[] boxes = new HashSet[9];

        // Initialize the hash sets
        for (int i = 0; i < 9; i++) {
            rows[i] = new HashSet<>();
            cols[i] = new HashSet<>();
            boxes[i] = new HashSet<>();
        }

        // Iterate through the board
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                char num = board[i][j];
                if (num == '.') continue; // Skip empty cells

                // Check the row
                if (rows[i].contains(num)) return false;
                rows[i].add(num);

                // Check the column
                if (cols[j].contains(num)) return false;
                cols[j].add(num);

                // Check the sub-box
                int boxIndex = (i / 3) * 3 + (j / 3);
                if (boxes[boxIndex].contains(num)) return false;
                boxes[boxIndex].add(num);
            }
        }

        return true;
    }
}
```
