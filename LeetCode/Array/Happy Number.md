# [Happy Number](https://leetcode.com/problems/happy-number/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Hash Table`, `Math`, `Two Pointers`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/d7c90d5f-494c-4d8e-a980-2a8df503c3ec)
## Solution (Incomplete)
```java
class Solution {
    public boolean isHappy(int n) {
        if (n == 1) return true;
        // what if it never becomes 1, it means it will be stuck in an infinite loop.
        // some values have to be repeated for a loop to exist.
        if {
            int sum = 0;
            while (n > 0) {
                sum += Math.pow(n%10, 2)
                n = n / 10;
            }
            return isHappy(sum);
        }
        return false;
    }
}
```
---
## Solution (Hash Set)
```java
import java.util.HashSet;
import java.util.Set;

public class Solution {
    public boolean isHappy(int n) {
        Set<Integer> seen = new HashSet<>();
        
        while (n != 1 && !seen.contains(n)) {
            seen.add(n);
            int sum = 0;
            while (n > 0) {
                int digit = n % 10;
                sum += digit * digit;
                n /= 10;
            }
            n = sum;
        }
        
        return n == 1;
    }
}
```
---
## Solution (Two Pointers)
```java
public class Solution {
    public boolean isHappy(int n) {
        int slow = n, fast = n;
        
        do {
            slow = getNext(slow);
            fast = getNext(getNext(fast));
        } while (slow != 1 && slow != fast);
        
        return slow == 1;
    }
    
    private int getNext(int n) {
        int sum = 0;
        while (n > 0) {
            int digit = n % 10;
            sum += digit * digit;
            n /= 10;
        }
        return sum;
    }
}
```
