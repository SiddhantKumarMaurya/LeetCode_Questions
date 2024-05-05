# [Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/description/)
## Topics: `Linked List`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/2cfbe0b1-b46c-4fc7-bee3-162830c6ba9a)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/5a77f9d5-8dae-484b-a2c9-d38ba06065ad)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/03e8b0a5-778c-434c-a899-dc5b27361d22)
## Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        ListNode previousNode = node;
        ListNode currentNode = node;
        ListNode nextNode = node.next;
        while(nextNode != null) {
            int temp = node.val;
            node.val = nextNode.val;
            nextNode.val = temp;
            previousNode = node;
            node = nextNode;
            nextNode = nextNode.next;
        }
        previousNode.next = node.next;
    }
}
```
