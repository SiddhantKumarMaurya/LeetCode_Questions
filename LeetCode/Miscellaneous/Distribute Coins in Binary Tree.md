# [Distribute Coins in Binary Tree](https://leetcode.com/problems/distribute-coins-in-binary-tree/description/?envType=daily-question&envId=2024-05-18)
## Topics: `Tree`, `Depth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/737c3ca9-1d28-466c-96ca-7021843a9311)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b91a1cc1-d9f4-419a-af50-d8f7dc329698)
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
    int moves = 0;

    public int distributeCoins(TreeNode root) {
        postOrder(root);
        return moves;
    }

    public int postOrder(TreeNode root) {
        if (root == null) return 0;

        int left = postOrder(root.left);
        int right = postOrder(root.right);

        int excess = left + right + root.val - 1;

        moves += Math.abs(excess);
        return excess;

    }
}
```
