# [Number of Steps to Reduce a Number in Binary Representation to One](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one/description/?envType=daily-question&envId=2024-05-29)
## Topics: `String`, `Bit Manipulation`
## Problem Satatement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/6deca11d-aafc-4dbf-bcab-4011bc213fd6)
## Solution (Correct Approach, but it could not handle very long binary stringa)
```java
class Solution {
    public int numSteps(String s) {
        int count = 0;
        long num = Long.parseLong(s, 2);
        while (num != 1) {
            count++;
            if (num % 2 == 0) {
                num = num / 2;
                s = "" + num;
            } else {
                num++;
                s = "" + num;
            }
        }
        return count;
    }
}
```
---
## Solution (Correct, but too slow)
```java
import java.math.BigInteger;

class Solution {
    public int numSteps(String s) {
        int count = 0;
        BigInteger num = new BigInteger(s, 2);
        while (!num.equals(BigInteger.ONE)) {
            count++;
            if (num.mod(BigInteger.TWO).equals(BigInteger.ZERO)) {
                num = num.divide(BigInteger.TWO);
            } else {
                num = num.add(BigInteger.ONE);
            }
        }
        return count;
    }
}
```
## Solution
```java
class Solution {
    public int numSteps(String s) {
        int res = 0, carry = 0;

        for(int i = s.length() - 1; i> 0; i--){
            res++;
            if(s.charAt(i) - '0' + carry == 1){
                carry = 1;
                res ++;
            }

        }

        return res + carry;
    }
}
```
