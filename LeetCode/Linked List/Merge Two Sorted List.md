# [Merge Two Sorted List](https://leetcode.com/problems/merge-two-sorted-lists/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Linked List`, `Recursion`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/95f812ef-bd53-43f8-8fd7-d4d2b68046bc)
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
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode newList =new  ListNode();
        ListNode head = newList;

        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                newList.next = new ListNode(list1.val);
                newList = newList.next;
                list1 = list1.next;
            } else {
                newList.next = new ListNode(list2.val);
                newList = newList.next;
                list2 = list2.next;
            }
        }

        while (list1 != null) {
            newList.next = new ListNode(list1.val);
            newList = newList.next;
            list1 = list1.next;
        }

        while (list2 != null) {
            newList.next = new ListNode(list2.val);
            newList = newList.next;
            list2 = list2.next;
        }

        return head.next;
    }
}
````
