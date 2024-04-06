# [Game of Life](https://leetcode.com/problems/game-of-life/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Matrix`, `Simulation`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/32ccde0e-d731-4ce9-b8a0-d8c8ba537b53)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/96936ccc-39c2-4ce0-85a0-3b8e29feef8a)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/61db6274-9e00-4eb0-ab62-588f4760fdec)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/599aaec3-a9c0-4fd2-8951-95a8602354d8)
## Solution
```java
import java.util.List;
class Solution {
    public void gameOfLife(int[][] board) {
        List<List<Integer>> list = new ArrayList<>();

        int row = board.length;
        int column = board[0].length;

        // Corner Cases
        if (row == 1)
        {
            if (column == 1) {
                board[0][0] = 0;
                return;
            }
            else if (column == 2) {
                board[0][0] = 0;
                board[0][1] = 0;
                return;
            }
            else {
                ArrayList<Integer> arrlist = new ArrayList<>();
                for (int i = 1; i < column - 1; i++) {
                    if (board[0][i - 1] + board[0][i + 1] == 2) {
                        if (board[0][i] == 1) arrlist.add(i);
                    } 
                }
                int k = 0;
                int length = arrlist.size();
                for (int i = 0; i < column; i++) {
                    if (k < length && i == arrlist.get(k)) {
                        board[0][i] = 1;
                        k++;
                    } else board[0][i] = 0;
                }
                return;
            }
        }  

        // Corner Cases
        if (column == 1) {
            if (row == 2) {
                board[0][0] = 0;
                board[1][0] = 0;
                return;
            } else {
                ArrayList<Integer> arrlist = new ArrayList<>();
                for (int i = 1; i < row - 1; i++) {
                    if (board[i - 1][0] + board[i + 1][0] == 2) {
                        if (board[i][0] == 1) arrlist.add(i);
                    } 
                }
                int k = 0;
                int length = arrlist.size();
                for (int i = 0; i < row; i++) {
                    if (k < length && i == arrlist.get(k)) {
                        board[i][0] = 1;
                        k++;
                    } else board[i][0] = 0;
                }
                return;
            }
        }

        int neighbours = 0;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < column; j++) {
                int currentState = board[i][j];
                if (i == 0 && j == 0) {
                    neighbours = board[i][j + 1] + board[i + 1][j + 1] + board[i + 1][j];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else if (i == 0 && j == column - 1) {
                    neighbours = board[i][j - 1] + board[i + 1][j - 1] + board[i + 1][j];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else if (i == row - 1 && j == 0) {
                    neighbours = board[i][j + 1] + board[i - 1][j + 1] + board[i - 1][j];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else if (i == row - 1 && j == column - 1) {
                    neighbours = board[i][j - 1] + board[i - 1][j - 1] + board[i - 1][j];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else if (i == 0) {
                    neighbours =board[i][j - 1] + board[i + 1][j - 1] + board[i][j + 1] + board[i + 1][j + 1] + board[i + 1][j];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else if (j == 0) {
                    neighbours = board[i - 1][j] + board[i - 1][j + 1] + board[i][j + 1] + board[i + 1][j + 1] + board[i + 1][j];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else if (i == row - 1) {
                    neighbours = board[i][j - 1] + board[i - 1][j - 1] + board[i - 1][j] + board[i][j + 1] + board[i - 1][j + 1];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else if (j == column - 1) {
                    neighbours = board[i + 1][j] + board[i + 1][j - 1] + board[i][j - 1] + board[i - 1][j - 1] + board[i - 1][j];
                    decideNextGen(list, neighbours,currentState, i, j);
                } else {
                    neighbours = board[i - 1][j - 1] + board[i - 1][j] + board[i - 1][j + 1] + board[i][j - 1] + board[i][j + 1] + board[i + 1][j - 1] + board[i + 1][j] + board[i + 1][j + 1];
                    decideNextGen(list, neighbours,currentState, i, j);
                }
            }
        }

        int length = list.size();
        int k = 0;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < column; j++) {
                if (k < length && i == list.get(k).get(0) && j == list.get(k).get(1)) {
                    board[i][j] = 1;
                    k++;
                } else board[i][j] = 0;
            }
        }
    }
    
    public void decideNextGen(List<List<Integer>> list, int neighbours,int currentState, int i, int j) {
        if (currentState == 0) {
            if (neighbours == 3) {
                addIndex(list, i, j);
            }
        } else if (currentState == 1) {
            if (neighbours == 2 || neighbours == 3) {
                addIndex(list, i, j);
            }
        }
    }

    public void addIndex(List<List<Integer>> list, int i, int j) {
        ArrayList<Integer> arrayList = new ArrayList<>();
        arrayList.add(i);
        arrayList.add(j);
        list.add(arrayList);
    }
}
```
---
## Solution
```java
// This algorithm is called "Conway's Game of Life." It is a cellular automaton devised by the British mathematician John Horton Conway in 1970. The game is a zero-player game, meaning that its evolution is determined by its initial state, requiring no further input. Players interact with the Game of Life by creating an initial configuration and observing how it evolves according to a set of rules.
class Solution {
    public void gameOfLife(int[][] board) {
        int m = board.length;
        int n = board[0].length;
        
        // Create a copy of the board to store the next state
        int[][] nextState = new int[m][n];
        
        // Iterate through each cell in the original board
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // Count the number of live neighbors
                int liveNeighbors = countLiveNeighbors(board, i, j);
                
                // Apply the rules of the Game of Life
                if (board[i][j] == 1) {
                    if (liveNeighbors < 2 || liveNeighbors > 3) {
                        nextState[i][j] = 0; // Any live cell with fewer than two live neighbors or more than three live neighbors dies
                    } else {
                        nextState[i][j] = 1; // Any live cell with two or three live neighbors lives on to the next generation
                    }
                } else {
                    if (liveNeighbors == 3) {
                        nextState[i][j] = 1; // Any dead cell with exactly three live neighbors becomes a live cell
                    }
                }
            }
        }
        
        // Copy the next state from the copy of the board back to the original board
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = nextState[i][j];
            }
        }
    }
    
    // Helper method to count live neighbors for a given cell
    private int countLiveNeighbors(int[][] board, int row, int col) {
        int count = 0;
        int m = board.length;
        int n = board[0].length;
        
        int[] dx = {-1, -1, -1, 0, 0, 1, 1, 1};
        int[] dy = {-1, 0, 1, -1, 1, -1, 0, 1};
        
        for (int k = 0; k < 8; k++) {
            int x = row + dx[k];
            int y = col + dy[k];
            if (x >= 0 && x < m && y >= 0 && y < n && board[x][y] == 1) {
                count++;
            }
        }
        
        return count;
    }
}
```
