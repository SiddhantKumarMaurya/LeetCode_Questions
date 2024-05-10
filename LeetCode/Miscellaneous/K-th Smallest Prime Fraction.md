# [K-th Smallest Prime Fraction](https://leetcode.com/problems/k-th-smallest-prime-fraction/description/?envType=daily-question&envId=2024-05-10)
## Topics: `Array`, `Two Pointers`, `Binary Search`, `Sorting`, `Heap (Priority Queue)`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/52e899e6-a05b-49ac-832b-dabad4bbcff0)
## Solution
```java
class Solution {
    public int[] kthSmallestPrimeFraction(int[] arr, int k) {
        int n = arr.length;
        double low = 0, high = 1;
        
        while (low < high) {
            double mid = (low + high) / 2;
            int count = 0;
            double maxFraction = 0;
            int numerator = 0, denominator = 1;
            
            for (int i = 0, j = 1; i < n - 1; i++) {
                while (j < n && arr[i] > mid * arr[j]) {
                    j++;
                }
                count += n - j;
                if (j < n && maxFraction < (double)arr[i] / arr[j]) {
                    maxFraction = (double)arr[i] / arr[j];
                    numerator = arr[i];
                    denominator = arr[j];
                }
            }
            
            if (count == k) {
                return new int[]{numerator, denominator};
            } else if (count < k) {
                low = mid;
            } else {
                high = mid;
            }
        }
        
        return new int[0]; // Not found
    }
}
```
