## [Gas Station](https://leetcode.com/problems/gas-station/?envType=study-plan-v2&envId=top-interview-150)
## Solution:
### Intitial Thoughts:
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int stations = gas.length;
        int start = 0;
        int station = 0;
        for (station = 0; station < stations; station++) {
            if (gas[station] > cost[station]){
                start = station;
                break;
            }
        }

        if (station == stations) return -1;

        int j = start;
        int tank = 0;
        while (true) {
            int pay = cost[j];
            tank = tank + gas[j]; 
            
            j = (j + 1) % stations;
            if (j == start) return start;

            if (tank < pay) return -1;
            
            tank = tank - pay;
        }
    }
}
```
#### Problem with the above logic: 
1. *I was only checking if the tank had enough fuel to travel to the next station*
2. *What if the total fuel from the current station and the next station does not help us make it to the third station?*
3. *Thus we need to calculate total fuel and change the starting station accordingly*

### Final Solution:
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int totalGas = 0, totalCost = 0, tank = 0, start = 0;

        for (int i = 0; i < gas.length; i++) {
            totalGas += gas[i];
            totalCost += cost[i];
            tank += gas[i] - cost[i];
            
            // If tank becomes negative, reset the start position
            if (tank < 0) {
                start = i + 1;
                tank = 0;
            }
        }

        // Check if completing the circuit is possible
        return totalGas >= totalCost ? start : -1;
    }
}
```
