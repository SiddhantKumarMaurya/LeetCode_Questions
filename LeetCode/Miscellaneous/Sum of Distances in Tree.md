# [Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/description/)
## Topics: `Dynamic Programming`, `Tree`, `Depth-First Search`, `Graph`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/e8ae47f6-fe0a-475e-a22b-fc5ca3fd70ad)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c30398bf-fc1c-4013-8862-85982b0ba313)
## Solution
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public int[] sumOfDistancesInTree(int n, int[][] edges) {
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adjList.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            adjList.get(edge[0]).add(edge[1]);
            adjList.get(edge[1]).add(edge[0]);
        }

        int[] count = new int[n];
        int[] distanceSum = new int[n];

        // First DFS to compute count and sum of distances for each node
        dfs1(0, -1, adjList, count, distanceSum);

        // Second DFS to update sum of distances for each node considering it as a child of its parent
        dfs2(0, -1, adjList, count, distanceSum, n);

        return distanceSum;
    }

    private void dfs1(int node, int parent, List<List<Integer>> adjList, int[] count, int[] distanceSum) {
        count[node] = 1;
        for (int child : adjList.get(node)) {
            if (child == parent) continue;
            dfs1(child, node, adjList, count, distanceSum);
            count[node] += count[child];
            distanceSum[node] += distanceSum[child] + count[child];
        }
    }

    private void dfs2(int node, int parent, List<List<Integer>> adjList, int[] count, int[] distanceSum, int n) {
        for (int child : adjList.get(node)) {
            if (child == parent) continue;
            distanceSum[child] = distanceSum[node] - count[child] + n - count[child];
            dfs2(child, node, adjList, count, distanceSum, n);
        }
    }
}
```
