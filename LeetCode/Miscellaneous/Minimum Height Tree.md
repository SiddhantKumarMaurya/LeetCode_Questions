# [Minimum Height Tree](https://leetcode.com/problems/minimum-height-trees/description/)
## Topics: `Depth-First Search`, `Breadth-First Search`, `Graph`, `Topological Sort`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/83e7a2d6-a155-4a3e-80a5-6b8ff61db616)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/fa93eea6-8541-4344-9407-11eb70a16c13)
## Solution
```java
import java.util.*;

class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        if (n == 1) {
            return Collections.singletonList(0); // Single node tree
        }

        List<Set<Integer>> adjList = new ArrayList<>(n);
        for (int i = 0; i < n; i++) {
            adjList.add(new HashSet<>());
        }

        for (int[] edge : edges) {
            adjList.get(edge[0]).add(edge[1]);
            adjList.get(edge[1]).add(edge[0]);
        }

        Queue<Integer> leaves = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (adjList.get(i).size() == 1) {
                leaves.offer(i); // Add leaf nodes to the queue
            }
        }

        while (n > 2) {
            int numLeaves = leaves.size();
            n -= numLeaves;
            for (int i = 0; i < numLeaves; i++) {
                int leaf = leaves.poll();
                int neighbor = adjList.get(leaf).iterator().next(); // Get the neighbor
                adjList.get(neighbor).remove(leaf); // Remove the edge between leaf and neighbor
                if (adjList.get(neighbor).size() == 1) {
                    leaves.offer(neighbor); // Add neighbor to the queue if it becomes a leaf
                }
            }
        }

        return new ArrayList<>(leaves); // Remaining nodes are the roots of MHTs
    }
}
```
