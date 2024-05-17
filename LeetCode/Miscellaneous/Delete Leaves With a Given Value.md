# [Delete Leaves With a Given Value](https://leetcode.com/problems/delete-leaves-with-a-given-value/description/?envType=daily-question&envId=2024-05-17)
## Topics: `Tree`, `Depth-First Search`, `Binary Tree`
## Problem Statement:
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/f3a9ec38-d3fa-4e4e-9396-1d7d2a54d2da)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/3ad6641a-12c0-40aa-94d0-7133a3525f30)
## Solution:
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
public class Solution {
    public TreeNode removeLeafNodes(TreeNode root, int target) {
        // Helper function to recursively remove target leaf nodes
        return removeLeaves(root, target);
    }

    private TreeNode removeLeaves(TreeNode node, int target) {
        // Base case: if node is null, return null
        if (node == null) {
            return null;
        }

        // Recursively process the left and right children
        node.left = removeLeaves(node.left, target);
        node.right = removeLeaves(node.right, target);

        // If the current node becomes a leaf and its value is target, remove it
        if (node.left == null && node.right == null && node.val == target) {
            return null;
        }

        // Otherwise, return the current node
        return node;
    }
}
```
