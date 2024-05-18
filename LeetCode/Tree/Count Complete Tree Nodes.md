## [Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Binary Search`, `Bit Manipulation`, `Tree`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ab0358d0-e756-4876-8721-546c06c892b7)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/3011c57b-6fea-46e7-9812-59fa43ea1e0c)
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
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int height = getHeight(root);
        if (height == 0) {
            return 1;
        }

        int left = 0, right = (1 << height) - 1; // 2^height - 1
        while (left < right) {
            int mid = (left + right + 1) / 2;
            if (exists(mid, height, root)) {
                left = mid;
            } else {
                right = mid - 1;
            }
        }
        return (1 << height) - 1 + left + 1; // 2^height - 1 + left + 1
    }

    private int getHeight(TreeNode node) {
        int height = 0;
        while (node.left != null) {
            height++;
            node = node.left;
        }
        return height;
    }

    private boolean exists(int index, int height, TreeNode node) {
        int left = 0, right = (1 << height) - 1; // 2^height - 1
        for (int i = 0; i < height; i++) {
            int mid = (left + right) / 2;
            if (index <= mid) {
                node = node.left;
                right = mid;
            } else {
                node = node.right;
                left = mid + 1;
            }
        }
        return node != null;
    }
}
```
