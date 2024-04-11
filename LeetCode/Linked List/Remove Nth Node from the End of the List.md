# [Remove Nth Node from the End of the List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Linked List`, `Two Pointers`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/154f9c69-5ecb-4367-b261-81122e8dc9ba)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c161d777-751e-4532-ab3d-dc6c752c7881)
## Solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int i = 0;
        ListNode temp = head;
        int length = 0;
        while(temp != null) {
            length++;
            temp = temp.next;
        }

        if (head.next == null && n == 1) return null;

        // in case we need to remove head
        if (length == n) {
            head = head.next;
            return head;
        }  
        ListNode currentNode = null;
        ListNode nextNode = head;
        while(i < length - n) {
            currentNode = nextNode;
            nextNode = nextNode.next;
            i++;
        }
        currentNode.next = nextNode.next;
        nextNode.next = null;
        return head;
    }
}
```
---
## Solution (In one pass)
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // Create a dummy node to handle edge cases
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        // Initialize two pointers
        ListNode first = dummy;
        ListNode second = dummy;

        // Move the second pointer forward by n+1 steps
        for (int i = 0; i <= n; i++) {
            second = second.next;
        }

        // Move both pointers simultaneously until the second pointer reaches the end
        while (second != null) {
            first = first.next;
            second = second.next;
        }

        // Remove the nth node from the end by updating the next reference of the first pointer
        first.next = first.next.next;

        return dummy.next;
    }
}
```
