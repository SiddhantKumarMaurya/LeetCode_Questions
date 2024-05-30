# [Count Triplets That Can Form Two Arrays of Equal XOR](https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor/description/)
## Topics: `Array`, `Hash Table`, `Math`, `Bit Manipulation`, `Prefix Sum`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/7c733f7e-51c3-41df-8471-389729b978c9)
## Solution
```java
class Solution {
    public int countTriplets(int[] arr) {
        int n = arr.length;
        int[] prefixXor = new int[n + 1];

        // Compute prefix XOR array
        for (int i = 0; i < n; i++) {
            prefixXor[i + 1] = prefixXor[i] ^ arr[i];
        }

        int count = 0;

        // Iterate through all pairs (j, k) with j < k
        for (int j = 0; j < n; j++) {
            for (int k = j + 1; k < n; k++) {
                if (prefixXor[j] == prefixXor[k + 1]) {
                    count += k - j;
                }
            }
        }

        return count;
    }
}
```
