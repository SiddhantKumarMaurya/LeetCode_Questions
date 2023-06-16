# [Richest Customer Wealth](https://leetcode.com/problems/richest-customer-wealth/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/09d76dbb-998c-41ae-b983-dd5ecae05448)
## Solution
```java
class Solution {
    public int maximumWealth(int[][] accounts) {
        int wealth = 0;
        int tempWealth = 0;
        int row = accounts.length;
        int columns = accounts[0].length;

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < columns; j++) {
                tempWealth = tempWealth + accounts[i][j];
            }
            if (wealth < tempWealth) {
                wealth = tempWealth;
            }
            tempWealth = 0;
        }
        return wealth;
    }
}
```
