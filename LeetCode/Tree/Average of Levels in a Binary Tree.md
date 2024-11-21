# [Average of Levels in a Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/description/?envType=study-plan-v2&envId=top-interview-150)
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

 import java.util.List;
 import java.util.ArrayList;
 import java.util.Queue;

class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> result = new ArrayList<>();
        if (root == null) return result;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            long sum = 0; // Use long to prevent overflow

            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                sum += node.val;

                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }

            //Calculate the average for this level
            result.add(sum * 1.0 / levelSize);
        }

        return result;
    }
}
```
