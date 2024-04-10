# [Reveal Cards in Increasing Order](https://leetcode.com/problems/reveal-cards-in-increasing-order/description/?envType=daily-question&envId=2024-04-10)
## Topics: `Array`, `Queue`, `Sorting`, `Simulation`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/1dc27745-48ea-4992-9ba3-772a50adf2c0)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/e6da72ed-6db0-4dd2-a2ce-6ca11ab8f9be)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/72a3e60b-b10d-476c-acfa-4b05d4813f78)
## Solution
```java
import java.util.Arrays;
class Solution {
    public int[] deckRevealedIncreasing(int[] deck) {
        int length = deck.length;
        Arrays.sort(deck);
        if (length <= 2) return deck;
        int[] auxArray = new int[length * 2];;
        for (int i = 0, j = 0; i < length * 2; i += 2) {
            auxArray[i] = deck[j];
            j++;
        }

        int lengthOfAux = length * 2 - 1;

        int i = lengthOfAux - 1;
        int j = i - 3;

        int temp = auxArray[i];
        auxArray[i] = auxArray[j];
        auxArray[j] = temp;

        j -= 2;
        i -= 2;

        while (j > 0 && auxArray[j] == 0) {
            temp = auxArray[i];
            auxArray[i] = auxArray[j];
            auxArray[j] = temp; 
            i --;
            j -= 2;
            lengthOfAux--;
        }

        for (int k = 0; k < length; k++) {
            deck[k] = auxArray[k];
        }
        return deck;
    }
}
```
