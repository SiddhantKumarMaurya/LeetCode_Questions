# [Time Needed to Buy Tickets](https://leetcode.com/problems/time-needed-to-buy-tickets/description/?envType=daily-question&envId=2024-04-09)
## Topics: `Array`, `Queue`, `Simulation`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/2c64532c-d35f-49f4-8a0b-76f7bb1247d5)
## Solution
```java
class Solution {
    public int timeRequiredToBuy(int[] tickets, int k) {
        int ticketsToBuy = tickets[k];
        int length = tickets.length;
        int totalTime = 0;
        for (int i = 0; i < length; i++) {
            if (i < k) {
                // time taken by people in queue before the ith person to buy tickets equal to k
                totalTime += Math.min(tickets[i], ticketsToBuy);
            } else if (i > k) {
                // time taken by people in queue after the ith person to buy tickets equal to k - 1
                totalTime += Math.min(tickets[i], ticketsToBuy - 1);
            }
            
        }

        // total wait time + time taken by ith person
        return totalTime + ticketsToBuy;
  }
}
```
