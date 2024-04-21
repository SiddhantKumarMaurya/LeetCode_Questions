# [Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/description/)
## Topics: `Depth-First Search`, `Breadth-First Search`, `Union Find`, `Graph`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/499e00c5-64de-4a5a-88ee-7c5a62306c19)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/1e95f246-3e4c-4a0a-bde0-bbe2b5cdadff)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ff520a62-8899-4904-adc2-edc43e042446)
## Solution
```java
import java.util.*;

class Solution {
    public boolean validPath(int n, int[][] edges, int source, int destination) {
        // Build adjacency list representation of the graph
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adjList.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            adjList.get(u).add(v);
            adjList.get(v).add(u);
        }
        
        // Initialize visited array
        boolean[] visited = new boolean[n];
        
        // Perform DFS starting from source vertex
        return dfs(adjList, visited, source, destination);
    }
    
    private boolean dfs(List<List<Integer>> adjList, boolean[] visited, int source, int destination) {
        // Mark current vertex as visited
        visited[source] = true;
        
        // If the destination vertex is reached, return true
        if (source == destination) {
            return true;
        }
        
        // Explore neighboring vertices
        for (int neighbor : adjList.get(source)) {
            if (!visited[neighbor]) {
                if (dfs(adjList, visited, neighbor, destination)) {
                    return true;
                }
            }
        }
        
        // If destination vertex is not found, return false
        return false;
    }
}
```
