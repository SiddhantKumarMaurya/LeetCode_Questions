# [Add One Row to Tree](https://leetcode.com/problems/add-one-row-to-tree/description/)
## Topics: `Tree`, `Depth-First Search`, `Breadth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/363eebbb-d7ab-4ff0-bcff-deff82017da8)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/e8bfbdf7-e8ac-42f2-b6d4-ea5ac23273d3)
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
    public TreeNode addOneRow(TreeNode root, int val, int depth) {
        if (depth == 1) {
            TreeNode newNode = new TreeNode(val);
            newNode.left = root;
            return newNode;
        }
        helper(root, val, depth, 1);
        return root;
    }

    private void helper(TreeNode root, int val, int depth, int currentDepth) {
        if (currentDepth == depth - 1) {
            TreeNode newLeftNode = new TreeNode(val);
            TreeNode newRightNode = new TreeNode(val);
            if (root != null) {
                newLeftNode.left = root.left;
                newRightNode.right = root.right;
                root.left = newLeftNode;
                root.right = newRightNode;
            }
            return;
        }
        if (root != null) {
            helper(root.left, val, depth, currentDepth + 1);
            helper(root.right, val, depth, currentDepth + 1);
        }
    }
}
```
