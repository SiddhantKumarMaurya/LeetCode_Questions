# [Minimum Cost to Hire K Workers](https://leetcode.com/problems/minimum-cost-to-hire-k-workers/description/?envType=daily-question&envId=2024-05-11)
## Topics: `Array`, `Greedy`, `Sorting`, `Heap (Priority Queue)`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/0db90360-7487-4f79-8895-b4d47043ea8e)
## Solution
```java
import java.util.Arrays;
import java.util.PriorityQueue;

class Worker implements Comparable<Worker> {
    int quality;
    double ratio;

    public Worker(int quality, int wage) {
        this.quality = quality;
        this.ratio = (double) wage / quality;
    }

    @Override
    public int compareTo(Worker other) {
        return Double.compare(this.ratio, other.ratio);
    }
}

public class Solution {
    public double mincostToHireWorkers(int[] quality, int[] wage, int k) {
        int n = quality.length;
        Worker[] workers = new Worker[n];
        for (int i = 0; i < n; i++) {
            workers[i] = new Worker(quality[i], wage[i]);
        }
        Arrays.sort(workers);

        PriorityQueue<Integer> maxQualityHeap = new PriorityQueue<>((a, b) -> b - a);
        int totalQuality = 0;
        double minTotalWage = Double.MAX_VALUE;

        for (Worker worker : workers) {
            maxQualityHeap.offer(worker.quality);
            totalQuality += worker.quality;

            if (maxQualityHeap.size() > k) {
                totalQuality -= maxQualityHeap.poll();
            }

            if (maxQualityHeap.size() == k) {
                minTotalWage = Math.min(minTotalWage, totalQuality * worker.ratio);
            }
        }

        return minTotalWage;
    }
}
```
