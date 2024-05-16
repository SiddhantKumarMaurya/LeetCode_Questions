# [Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Tree`, `Depth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b062afcf-f5e3-452a-8979-676d61703f07)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b38b5565-faf7-4efd-a744-1b9c6747f626)
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
    public int sumNumbers(TreeNode root) {
        return sumHelper(root, 0);
    }

    public int sumHelper(TreeNode root, int sum) {
        if (root == null) return 0;

        sum = sum * 10 + root.val;

        if (root.left == null && root.right == null) {
            return sum;
        }

        int leftSum = sumHelper(root.left, sum);
        int rightSum = sumHelper(root.right, sum);

        return leftSum + rightSum;
    }
}
```
