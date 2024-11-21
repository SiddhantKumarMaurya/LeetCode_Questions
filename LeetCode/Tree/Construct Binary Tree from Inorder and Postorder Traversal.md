# [Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/?envType=study-plan-v2&envId=top-interview-150)
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
import java.util.HashMap;
import java.util.Map;

class Solution {
    private Map<Integer, Integer> inorderIndexMap;
    private int postorderIndex;

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        // Build a hashmap to store value -> index relations for inorder traversal
        inorderIndexMap = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            inorderIndexMap.put(inorder[i], i);
        }

        // Initialize the postorder index to the last element
        postorderIndex = postorder.length - 1;

        return constructTree(postorder, 0, inorder.length - 1);
    }

    private TreeNode constructTree(int[] postorder, int left, int right) {
        // Base case: if there are no elements to construct the tree
        if (left > right) return null;

        // Select the current postorder index as the root and decrement it
        int rootValue = postorder[postorderIndex--];
        TreeNode root = new TreeNode(rootValue);

        // Build the right and left subtrees
        root.right = constructTree(postorder, inorderIndexMap.get(rootValue) + 1, right);
        root.left = constructTree(postorder, left, inorderIndexMap.get(rootValue) - 1);

        return root;
    }
}
```
