# [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d4261794-633f-40d9-875e-932b51c2530e)
## Solutions (Incomplete):
```java
// Initial logic but I did not finish it as I found a loop hole in the it
// loop hole: Lets say the pointOfPurchaseAndExpenditure[2] = prices.length - 1;
// then rest of the other prices will not be checked as we will be passing
// the value at second index of this array to function getProfit()
class Solution {
    int[] pointOfPurchaseAndExpenditure = new int[2];
    public int maxProfit(int[] prices) {
        int maxProfit = Integer.MAX_VALUE;
        int length = prices.length;
        int profitAtCurrentPrice = 0;
        int totalProfit = 0;
        for (int i = 0; i < length; i++) {
            profitAtCurrentPrice = getProfit(prices, i);
            
        }
    }

    public int getProfit(int[] prices, int startIndex) {
        pointOfPurchaseAndExpenditure[0] = startIndex;
        int potentialProfit = 0;
        int boughtAt = prices[startIndex];
        int length = prices.length;

        for (int i = startIndex + 1; i < length; i++) {
            currentPotentialProfit = prices[i] - boughtAt;

            // lets say that later the price drops to current price of the stock
            // then the currentPotentialProfit's value will be the same
            // In that case we might want to update our value of pointOfPurchaseAndExpenditure[1]
            // However, we have to increase the profit which means sell at the first sight of
            // low price thus the following contition check for both situations
            // if the price drops to the same value then make no changes.
            if (currentPotentialProfit > potentialProfit) {
                pointOfPurchaseAndExpenditure[1] = i;
                potentialProfit = currentPotentialProfit;
            }
        }

        return potentialProfit;
    }
}
```

## Solution (Incomplete)
```java
// Couldn't complete this one too. Logic was getting too complex.
class Solution {
    int maxProfit = 0;
    public int maxProfit(int[] prices) {
        int length = prices.length;
        for (int i = 0; i < length; i++) {
            maxProfit = Math.max(maxProfit, )
        }
    }

    public void getProfit(int[] prices, int soldAtDay) {
        if (soldAtDay == prices.length - 1) {
            return;
        }
        int potentialProfit = 0;
        int length = prices.length;
        int boughtAt = soldAtDay + 1;
        for (int i = soldAtDay + 2; i < length; i++) {
            if (prices[i] > boughtAt) {
                int currentPotentialProfit += prices[i] - boughtAt;
                potentialProfit = Math.max(potentialProfit, currentPotentialProfit);
                potentialProfit += getProfit(prices, i);
                maxProfit = Math.max(maxProfit, potentialProfit);
                
            }
        }
    }
}
```

## Solution (Time Limit Exceeds)
```java
class Solution {
    int maxProfit = 0;
    
    public int maxProfit(int[] prices) {
        getProfit(prices, 0, 0);
        return maxProfit;
    }

    public void getProfit(int[] prices, int day, int profitSoFar) {
        if (day >= prices.length) {
            maxProfit = Math.max(maxProfit, profitSoFar);
            return;
        }

        // Skip buying on this day and move to the next day
        getProfit(prices, day + 1, profitSoFar);

        // Try buying on this day and explore selling options on subsequent days
        for (int sellDay = day + 1; sellDay < prices.length; sellDay++) {
            if (prices[sellDay] > prices[day]) {
                int newProfit = profitSoFar + prices[sellDay] - prices[day];
                getProfit(prices, sellDay + 1, newProfit);
            }
        }
    }
}
```
## Solution (Greedy Approach)
```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            if (prices[i] < prices[i + 1]) {
                maxProfit += prices[i + 1] - prices[i];
            }
        }
        return maxProfit;
    }
}
```
The algorithm aims to maximize profit by making transactions whenever it's profitable to do so. Here's why this approach maximizes profit:

1. **Greedy Strategy**: The algorithm follows a greedy strategy, where it makes decisions based on the current situation without considering future consequences. In this case, it buys and sells stocks whenever it's profitable without looking ahead to future price movements.

2. **Optimal Substructure**: The problem exhibits optimal substructure, meaning that the optimal solution to the entire problem can be constructed from optimal solutions to its subproblems. In this case, the optimal solution for the entire sequence of days can be constructed by considering the optimal solution for each pair of consecutive days.

3. **Maximizing Local Profits**: By buying and selling whenever it's profitable on a day-by-day basis, the algorithm ensures that it maximizes the profit locally for each transaction. It captures all potential profits that can be made from the given prices.

4. **Proof by Contradiction**: If there exists a sequence of transactions that yields a higher profit than the one produced by this algorithm, it would mean that at least one transaction in the sequence was not made when it was profitable to do so, contradicting the greedy approach.

5. **Efficiency**: The algorithm has a time complexity of O(n), where n is the number of days, making it efficient for large inputs. This allows it to quickly find the maximum profit without exhaustive search or complex dynamic programming.

Overall, while there might exist situations where a different sequence of transactions could yield slightly higher profits, this greedy approach generally provides a practical and efficient solution that maximizes profit in most scenarios.
