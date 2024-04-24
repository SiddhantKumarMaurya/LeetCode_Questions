# [N-th Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number/description/)
## Topics: `Math`, `Dynamic Programming`, `Memoization`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/49187123-ecc1-4b40-9018-266228f9be40)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/a4baebbf-3327-44ba-8f23-df36bef2e289)
## Solution
```java
class Solution {
    public int tribonacci(int n) {
        int n0 = 0;
        int n1 = 1;
        int n2 = 1;

        if (n == 0) return n0;
        if (n == 1) return n1;
        if (n == 2) return n2;

        return tribonacci(n - 1) + tribonacci(n - 2) + tribonacci(n - 3);
    }
}
```
---
## Solution (Memoization)
```java
// lets use memoization this time
class Solution {
    public int tribonacci(int n) {
        // what if the n == 1 or n == 2;
        // array index out of bound on line number 6
        // that is why we have taken an array of length n + 3;
        int[] tribonacci = new int[n + 3];
        tribonacci[0] = 0;
        tribonacci[1] = 1;
        tribonacci[2] = 1;

        if (n == 0) return tribonacci[0];
        if (n == 1) return tribonacci[1];
        if (n == 2) return tribonacci[2];

        return helper(n, 3, tribonacci);
    }

    private int helper(int n, int i, int[] tribonacci) {
        if (i > n) return tribonacci[i - 1];
        tribonacci[i] = tribonacci[i - 1] + tribonacci[i - 2] + tribonacci[i - 3];
        return helper(n, i + 1, tribonacci);
    }
}
```
