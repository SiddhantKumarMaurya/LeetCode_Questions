# [Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/?envType=daily-question&envId=2024-04-15)
## Topics: `Tree`, `Depth-First Search`, `Binary Tree`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/da27d931-e482-4c05-b615-bd2a3fa65fa7)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b3e825fc-f46a-42bf-ad93-079cb1a8de88)
## Solution (Initial thought) (Incorrect)
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
        if (root == null) return 0;
        Stack<Integer> stack = new Stack<>();
        helper(root, stack);
        return stack.pop();
    }

    private void helper(TreeNode root, Stack<Integer> stack) {
        if (root == null) {
            String num = "";
            while (!stack.isEmpty() && stack.peek() < 10) {
                num = stack.pop() + num;
            }

            int sum = 0;
            if (!stack.isEmpty()) {
                if (num != "") {
                    sum = Integer.parseInt(num);
                }
                while (!stack.isEmpty()) {
                    sum = sum + stack.pop();
                }
                stack.push(sum);
            } else {
                sum = Integer.parseInt(num);
                stack.push(sum);
            }
            return;
        }

        stack.push(root.val);
        helper(root.left, stack);
        helper(root.right, stack);
    }
}
```
