# [Path Sum](https://leetcode.com/problems/path-sum/submissions/1258054120/)
## Topics: `Tree`, `Depth-First Search`, `Breadth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/bfe94ca2-f0e8-4042-9153-0e136dd08a22)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c13fad2c-58a2-4851-bc93-865025cb884f)
## Solution (Incorrect)
```java
// fails for test case:
// root = [1,2,null,3,null,4,null,5] (skewed binary tree)
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
    boolean isPathSum = false;
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        // remember a leaf is a node with no children, thus root = [1] is a leaf node
        // for root = [1]
        if (root.left == null && root.right == null) {
            if (root.val == targetSum) return true;
            else return false;
        }
        // for root = [1, 2]
        // here 1 is not a leaf node as it has on child thus only path 1 -> 2 can be said to be a valid path
        // 1 -> null (right child) is not valid
        if (root.left == null || root.right == null) {
            if (root.val == targetSum) return false;
        }
        helper(root, 0, targetSum);
        return isPathSum;
    }

    public void helper(TreeNode root, int sum, int targetSum) {
        if (root == null) {
            if (sum == targetSum) {
                isPathSum = true;
            }
        } else {
            sum = sum + root.val;
            helper(root.left, sum, targetSum);
            helper(root.right, sum, targetSum);
        }
    }
}
```
---
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
    boolean isPathSum = false;
    public boolean hasPathSum(TreeNode root, int targetSum) {
        return helper(root, 0, targetSum);
    }

    public boolean helper(TreeNode root, int sum, int targetSum) {
        if (root == null) return false;
        // condition for leaf node
        if (root.left == null && root.right == null) {
            return sum + root.val == targetSum;
        }
        sum += root.val;
        return helper(root.left, sum, targetSum) || helper(root.right, sum, targetSum);
    }
}
```
