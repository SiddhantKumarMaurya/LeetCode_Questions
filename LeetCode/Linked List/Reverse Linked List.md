# [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)
## Topics: `Linked List`, `Recursion`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/308b42ec-8fe0-4ce7-bb77-a535cceab1d4)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/c8eb5dab-64fd-403b-ac79-58b56b914fa9)
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/85f508e3-83c7-47a1-81a3-d334485a2825)
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
    public ListNode reverseList(ListNode head) {
        if (head == null) return head;
        if (head.next == null) return head;
        ListNode currentHead = head;
        ListNode newHead = head;
        ListNode temp = head;
        while(temp != null) {
            newHead = temp;
            temp = temp.next;
        }
        reverseHelper(head);
        head.next = null;
        return newHead;
    }

    public void reverseHelper(ListNode root) {
        if (root.next.next == null) {
            root.next.next = root;
            return;
        }
        reverseHelper(root.next);
        root.next.next = root;
    }
}
```
