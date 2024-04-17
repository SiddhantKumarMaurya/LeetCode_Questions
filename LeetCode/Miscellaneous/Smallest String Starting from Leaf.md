# [Smallest String Starting from Leaf](https://leetcode.com/problems/smallest-string-starting-from-leaf/description/)
## Topics: `String`, `Tree`, `Depth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/0c7be404-a5a2-4b5f-a4e5-881926321b2d)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/5614dd33-12c1-402c-9634-0745a0d2f8a1)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/4ece9c08-a810-4ccf-9209-e3229e0ae95f)
## Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    String smallestString = "~";
    
    public String smallestFromLeaf(TreeNode root) {
        dfs(root, new StringBuilder());
        return smallestString;
    }
    
    private void dfs(TreeNode node, StringBuilder path) {
        if (node == null) return;
        
        // Append the character represented by the node value to the current path
        path.append((char) ('a' + node.val));
        
        // If the current node is a leaf, update the smallest string if the current path is smaller
        if (node.left == null && node.right == null) {
            path.reverse();
            String currentString = path.toString();
            path.reverse(); // Restore the path
            if (currentString.compareTo(smallestString) < 0) {
                smallestString = currentString;
            }
        }
        
        // Continue DFS traversal for left and right children
        dfs(node.left, path);
        dfs(node.right, path);
        
        // Backtrack: remove the last character from the path
        path.deleteCharAt(path.length() - 1);
    }
}
```
