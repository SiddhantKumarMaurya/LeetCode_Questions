# [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statment
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/43243ee3-744f-4301-a192-066e9036f6ab)
## Solution (Incorrect)
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
class Solution {
    public int maxProfit(int[] prices) {
        int length = prices.length;
        int maxProfit = 0;
        for (int i = 0; i < length - 1; i++) {
            // Error: Arrays.asList() returns a List
            ArrayList<Integer> arrayList = new ArrayList<>(Arrays.asList(prices));
            ArrayList<Integer> copiedList = arrayList.subList(i + 1, arrayList.size());
            int maxPrice = Collections.max(copiedList);
            int currentProfit = maxPrice - prices[i];
            maxProfit = Math.max(currentProfit, maxProfit);
        }
        return maxProfit;
    }
}
```
## Solution
