# [Minimum Cost to Move Chips to The Same Position](https://leetcode.com/problems/minimum-cost-to-move-chips-to-the-same-position/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/1a1cfc25-80c2-4ba3-b442-dbbce9263da2)
## Solution
### Actual Solution
```java
// My logic:
// Move all the chips to all the positions one by one and compare the values of
// different costs and consider the smallest one

class Solution {
    public int minCostToMoveChips(int[] position) {
        int len = position.length;

        // To store the cost the actuall cost
        int cost = 0;

        // To store the cost to move to all the different positions one by one
        int tempCost = 0;

        // To calculate the difference between source and destination positions
        int difference = 0;

        // For destination position
        int i = 0;

        while(i<len) {

            // Destination position
            int pos = position[i];
        for (int j = 0; j < len; j++) {
            if (position[j] < pos) {

                // Destination position - source position
                difference = pos - position[j];
            }else {

                // Source position - destination position
                difference = position[j] - pos;
            }

            // Calculate the cost
            // Move the chips two positions at a time
            // If the chip is left to move one position at last then increment the value
            // of cost and if the chip has reached the destination don't increment cost
            if (difference > 0 && difference % 2 == 1) {
                tempCost++;
            }
        }

        // Assume cost for the first time
        if(cost == 0) {
                cost = tempCost;
            }
        
        // compare and update the vlue of actuall cost
        if (tempCost < cost && tempCost != 0) {
            cost = tempCost;
        }

        // To check for next position set tempCost to 0
        tempCost = 0;

        // To increment the destination position
        i++;
        }
        return cost;
    }
}
```
### Alternate Solution (Incomplete)
```java
class Solution {
    public int minCostToMoveChips(int[] position) {
        int len = position.length;
        int cost = 0;

        int pos = 0;
        int count = 0;
//         Count the maximum number of cheaps at a position
        for (int i = 0; i < len; i++) {
            int tempCount = 0;
            for (int j = 0; j < len; j++) {
                if (position[i] == position[j]) {
                    tempCount++;
                }
            }
            if (tempCount > count) {
                pos = position[i];
                count = tempCount;
            }
        }
// Move all the chips to the position that has maximum number of chips
        int difference = 0;
        for (int i = 0; i < len; i++) {
            if (position[i] != 0) {
                if (position[i] < pos) {
                difference = pos - position[i];
            }else {
                difference = position[i] - pos;
            }
            if (difference > 0 && difference % 2 == 1) {
                cost++;
                position[i] = 0;
            }
            }
        }
        return cost;
    }
}
```

