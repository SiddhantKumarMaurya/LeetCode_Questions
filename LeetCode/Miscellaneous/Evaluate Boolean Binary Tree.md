# [Evaluate Boolean Binary Tree](https://leetcode.com/problems/evaluate-boolean-binary-tree/description/?envType=daily-question&envId=2024-05-16)
## Topics: `Tree`, `Depth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/be0cdeef-92b6-48e8-b9e5-85be45ba6726)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/6989108b-e6f0-4b3c-9e25-d73417179fca)
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
    public boolean evaluateTree(TreeNode root) {
        // Base case: if the node is a leaf node
        if (root.left == null && root.right == null) {
            return root.val == 1;
        }
        
        // Recursive case: evaluate the left and right subtrees
        boolean leftValue = evaluateTree(root.left);
        boolean rightValue = evaluateTree(root.right);
        
        // Apply the boolean operation based on the node's value
        if (root.val == 2) { // OR operation
            return leftValue || rightValue;
        } else { // AND operation (root.val == 3)
            return leftValue && rightValue;
        }
    }
}
```
