# [Plus One](https://leetcode.com/problems/plus-one/)
```java
class Solution {
    public int[] plusOne(int[] digits) {
        int len = digits.length;
        int index = len - 1;
        // use carry to automate the process of addition over carry, if there is any carry
        int carry = 1;
        // use a loop to automate the chain of addition
        while (index >= 0) {
            // if the addition end in a number that's less than 10 then there's no
            // need to continue the addition
            if (digits[index] + carry < 10) {
            digits[index]++;
            return digits;
            }
            else {
                // if there is carry then propagate it to for the summation to the left
                // digit
                digits[index] = 0;
                carry = 1;
            }
            index--;
        }
        // in case if the number of digits of the given number increases after addition
        int newDigits[] = new int[len + 1];
        if (index == -1) {           
            newDigits[0] = 1;
            for (int i = 1; i < len + 1; i++) {
                newDigits[i] = digits[i - 1];
            }
        }
        return newDigits;
    }
}```
