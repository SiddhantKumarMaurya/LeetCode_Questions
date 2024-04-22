# [Open the Lock](https://leetcode.com/problems/open-the-lock/description/)
## Topics: `Array`, `Hash Table`, `String`, `Breadth-First Search`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/37881d5e-8d47-4372-bff4-85f15ad06aaa)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/bee1ba23-c137-46cf-9a8d-2ab33a2f90dc)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/a9d9c506-eb38-41c8-a806-f57441097f28)
## Solution
```java
import java.util.*;

class Solution {
    public int openLock(String[] deadends, String target) {
        Set<String> deadendsSet = new HashSet<>(Arrays.asList(deadends));
        if (deadendsSet.contains("0000")) {
            return -1; // The initial state is a deadend
        }
        
        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        queue.offer("0000");
        visited.add("0000");
        
        int turns = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String current = queue.poll();
                if (current.equals(target)) {
                    return turns;
                }
                List<String> nextStates = getNextStates(current);
                for (String nextState : nextStates) {
                    if (!deadendsSet.contains(nextState) && !visited.contains(nextState)) {
                        queue.offer(nextState);
                        visited.add(nextState);
                    }
                }
            }
            turns++;
        }
        
        return -1; // Target state not found
    }
    
    private List<String> getNextStates(String current) {
        List<String> nextStates = new ArrayList<>();
        for (int i = 0; i < 4; i++) {
            char[] currentState = current.toCharArray();
            char originalDigit = currentState[i];
            // Turn the wheel in both directions
            currentState[i] = (char) ((originalDigit - '0' + 1) % 10 + '0');
            nextStates.add(new String(currentState));
            currentState[i] = (char) ((originalDigit - '0' + 9) % 10 + '0');
            nextStates.add(new String(currentState));
        }
        return nextStates;
    }
}
```
