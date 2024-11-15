# [Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/?envType=study-plan-v2&envId=top-interview-150)
## Solution:
### Inital Thoughts:
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
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode temp = head;
        ListNode start = null;
        ListNode end = null;
        ListNode first = null;
        ListNode second;

        while(temp.val != right) {
            // java.lang.NullPointerException: Cannot read field "val" because "<local4>.next" is null
            // I did not check for any more errors after I got this error, but I think that the logic is correct.
            if (temp.next.val == left) first = temp;
            if (temp.val == left) {
                start = temp;
            }
            temp = temp.next;
        }

        if (temp.val == right) {
            end = temp;
        }

        second = temp.next;
        ListNode current = start;
        ListNode previous = null;

        reverse(current, previous);
        first.next = end;
        start.next = second;

        return head;

    }

    public void reverse(ListNode current, ListNode previous) {
        if (current.next == null) {
            return;
        }
        previous = current;
        current = current.next;
        reverse(current, previous);
        current.next = previous;
    }
}
```

#### Logic: Divid the list into three parts and reverse the middle one and then join them again.
#### Issues in code:
**Incorrect Conditions in the while Loop:**
The condition while (temp.val != right) is problematic because it can lead to a NullPointerException when traversing the list and temp becomes null.

**Incorrect Handling of first and second:**
You are assigning first and second based on the wrong logic. For example:
- first should be the node before start (the left-th node).
- second should be the node after end (the right-th node).

**The reverse Function Logic:**
- The reverse function is implemented incorrectly:
- It does not actually reverse the nodes. Instead, it ends up setting the current.next to the previous node only during recursive unwinding, leaving the rest of the list unchanged.

**Handling of Edge Cases:**
- Your code does not handle edge cases where:
 - left == 1 (reversing from the head of the list).
 - The list has only one node.

**Reconnecting the Sublist:**
- After reversing the sublist, you are incorrectly connecting first and start to end and second.
--------------
### Final Solution:
```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null || left == right) return head;

        // Dummy node to simplify edge cases
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;

        // Move `prev` to the node before the `left`-th node
        for (int i = 1; i < left; i++) {
            prev = prev.next;
        }

        // Start reversing the sublist
        ListNode current = prev.next;
        ListNode next = null;
        ListNode tail = current; // This will be the tail of the reversed sublist

        for (int i = 0; i < right - left + 1; i++) {
            next = current.next;
            current.next = prev.next;
            prev.next = current;
            current = next;
        }

        // Reconnect the sublist to the rest of the list
        tail.next = current;

        return dummy.next;
    }
}
```

