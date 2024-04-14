# [Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/description/)
## Topics: `Tree`, `Depth-First Search`, Breadth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/54fc5542-6044-4c68-abd5-ffdc0d68e27a)
## Solution (Incorrect)
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
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null || root.left == null) return 0;
        int sum = root.left.val;
        sum = sum + sumOfLeftLeaves(root.left);
        sum = sum + sumOfLeftLeaves(root.right);
        return sum;
    }
}
```

**didn't work for the case : [1,2,3,4,5]
output: 6;
expected output: 4;

Because I misunderstood the question. I had to find the sum of all the leaf nodes not all the left nodes. The above program is a solution for sum of all the left nodes.
**
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
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) return 0;
        int sum = 0;
        if (root.left != null && root.left.left == null && root.left.right == null) {
            // If the left child is a leaf node, add its value to the sum
            sum += root.left.val;
        }
        // Recursively traverse the left and right subtrees
        sum += sumOfLeftLeaves(root.left);
        sum += sumOfLeftLeaves(root.right);
        return sum;
    }
}
```
