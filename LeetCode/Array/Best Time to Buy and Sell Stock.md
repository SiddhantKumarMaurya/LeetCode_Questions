# [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
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
            //Error: (type error) ArrayList, List etc use wrapper class object: Integer, Double instead of int, double
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
## Solution (Incorrect)
```java
import java.util.List;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
class Solution {
    public int maxProfit(int[] prices) {
        int length = prices.length;
        int maxProfit = 0;
        // I use the following statement instead of manually copying all the emements into an Integer[].
        Integer[] copiedPrices = Arrays.stream(prices).boxed().toArray(Integer[]::new);
        for (int i = 0; i < length - 1; i++) {
            ArrayList<Integer> arrayList = new ArrayList<>(Arrays.asList(copiedPrices));
            // error: incompatible types: List<Integer> cannot be converted to ArrayList<Integer>
            ArrayList<Integer> copiedList = arrayList.subList(i + 1, arrayList.size());
            ArrayList<Integer> copiedList = arrayList.subList(i + 1, arrayList.size());
            int maxPrice = Collections.max(copiedList);
            int currentProfit = maxPrice - prices[i];
            maxProfit = Math.max(currentProfit, maxProfit);
        }
        return maxProfit;
    }
}
```

## Solution (Correct, but time limit exceeds)
```java
import java.util.List;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
class Solution {
    public int maxProfit(int[] prices) {
        int length = prices.length;
        int maxProfit = 0;
        // I use the following statement instead of manually copying all the emements into an Integer[].
        Integer[] copiedPrices = Arrays.stream(prices).boxed().toArray(Integer[]::new);
        for (int i = 0; i < length - 1; i++) {
            ArrayList<Integer> arrayList = new ArrayList<>(Arrays.asList(copiedPrices));
            // subList() returns a view of List.
            ArrayList<Integer> copiedList = new ArrayList(arrayList.subList(i + 1, arrayList.size()));
            int maxPrice = Collections.max(copiedList);
            int currentProfit = maxPrice - prices[i];
            maxProfit = Math.max(currentProfit, maxProfit);
        }
        return maxProfit;
    }
}
```

## Solution (Correct and Understandable, but time limit exceeds)
```java
import java.util.List;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;

class Solution {
    public int maxProfit(int[] prices) {
        int length = prices.length;
        int maxProfit = 0;
        Integer[] copiedPrices = Arrays.stream(prices).boxed().toArray(Integer[]::new);
        
        // Convert the Integer array to a List
        List<Integer> arrayList = Arrays.asList(copiedPrices);
        
        for (int i = 0; i < length - 1; i++) {
            // Create a new ArrayList from the List
            ArrayList<Integer> copiedList = new ArrayList<>(arrayList.subList(i + 1, arrayList.size()));
            int maxPrice = Collections.max(copiedList);
            int currentProfit = maxPrice - prices[i];
            maxProfit = Math.max(currentProfit, maxProfit);
        }
        return maxProfit;
    }
}
```

## Solution
```java
public class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE; // Initialize minPrice to maximum value
        int maxProfit = 0; // Initialize maxProfit to 0

        for (int price : prices) {
            // Update minPrice if current price is lower
            minPrice = Math.min(minPrice, price);
            // Update maxProfit if selling at current price gives more profit
            maxProfit = Math.max(maxProfit, price - minPrice);
        }

        return maxProfit;
    }
}
```
