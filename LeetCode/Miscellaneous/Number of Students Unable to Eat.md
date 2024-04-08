# [Number of Students Unable to Eat](https://leetcode.com/problems/number-of-students-unable-to-eat-lunch/description/?envType=daily-question&envId=2024-04-08)
## Topics: `Array`, `Stack`, `Queue`, `Simulation`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/253f6486-09e6-4321-8879-253cd3299f45)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/aca2813c-8449-4793-8ee3-7e45ad8f17fd)
## Solution (Incorrect)
```java
// Initial thought, I thought of keeping two variables 
// one to count total number of students who have ate so far
// and to count next total number of students who will have eaten in the next iteration
// (this was done to break out of loop in line number 30)
// but this logic has loop holes.
import java.util.ArrayList;
class Solution {
    public int countStudents(int[] students, int[] sandwiches) {
        int length = students.length;
        boolean[] ate = new boolean[length];
        int totalAte = 0;
        int nextTotalAte = 0;
        int i = 0;
        int j = 0;
        while (i < length) {
            while (j < length) {
                if (sandwiches[i] == students[j]) {
                    nextTotalAte++;
                    ate[j] = true;
                    j++;
                    i++;
                    break;
                }
                j++;
            }
            break;
        }
        
        while (i < length) {
            while (j < length && totalAte != nextTotalAte) {
                totalAte++;
                if (sandwiches[i] == students[j] && ate[j] != true) {
                    nextTotalAte++;
                    i++;
                    j++;
                    ate[j] = true;
                }
                j = (j + 1) % length;
            }
        }
        return (length - totalAte);
    }
}
```
----
## Solution
```java
import java.util.*;

class Solution {
    public int countStudents(int[] students, int[] sandwiches) {
        Queue<Integer> queue = new LinkedList<>();
        Stack<Integer> stack = new Stack<>();
        
        for (int student : students) {
            queue.offer(student);
        }
        
        for (int i = sandwiches.length - 1; i >= 0; i--) {
            stack.push(sandwiches[i]);
        }
        
        int unableToEat = 0;
        while (!queue.isEmpty()) {
            int student = queue.poll();
            int sandwich = stack.peek();
            
            if (student == sandwich) {
                stack.pop();
                unableToEat = 0; // Reset unableToEat counter
            } else {
                queue.offer(student);
                unableToEat++;
                
                // If all students in the queue cannot eat the current sandwich, break the loop
                if (unableToEat == queue.size()) {
                    break;
                }
            }
        }
        
        return queue.size();
    }
}
```
## Solution
```java
class Solution {
    public int countStudents(int[] students, int[] sandwiches) {
        int squareSandwichLover = 0;
        int circularSandwichLover = 0;
        int length = students.length;

        for (int i = 0; i < length; i++) {
            if (students[i] == 1) {
                squareSandwichLover++;
            } else {
                circularSandwichLover++;
            }
        }

        for (int i = 0; i < length; i++) {
            if (sandwiches[i] == 1 && squareSandwichLover > 0)
                squareSandwichLover--;
            else if(sandwiches[i] == 0 && circularSandwichLover > 0)
                circularSandwichLover--;
            else return squareSandwichLover + circularSandwichLover;
        }

        return 0;
        
    }
}
```
