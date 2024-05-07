# [Double a Number Represented as a Linked List](https://leetcode.com/problems/double-a-number-represented-as-a-linked-list/description/)
## Topics: `Linked List`, `Math`, `Stack`
## Problem Statement:
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/4629721b-ac85-44ae-a2bb-8daabcb60a9f)
## Solution (Reversing the List):
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
    public ListNode doubleIt(ListNode head) {
        // Reverse the linked list
        ListNode reversedList = reverseList(head);
        // Initialize variables to track carry and previous node
        int carry = 0;
        ListNode current = reversedList, previous = null;

        // Traverse the reversed linked list
        while (current != null) {
            // Calculate the new value for the current node
            int newValue = current.val * 2 + carry;
            // Update the current node's value
            current.val = newValue % 10;
            // Update carry for the next iteration
            if (newValue > 9) {
                carry = 1;
            } else {
                carry = 0;
            }
            // Move to the next node
            previous = current;
            current = current.next;
        }

        // If there's a carry after the loop, add an extra node
        if (carry != 0) {
            ListNode extraNode = new ListNode(carry);
            previous.next = extraNode;
        }

        // Reverse the list again to get the original order
        ListNode result = reverseList(reversedList);

        return result;
    }

    // Method to reverse the linked list
    public ListNode reverseList(ListNode node) {
        ListNode previous = null, current = node, nextNode;

        // Traverse the original linked list
        while (current != null) {
            // Store the next node
            nextNode = current.next;
            // Reverse the link
            current.next = previous;
            // Move to the next nodes
            previous = current;
            current = nextNode;
        }
        // Previous becomes the new head of the reversed list
        return previous;
    }
}
```
---
## Solution (Stack)
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
    public ListNode doubleIt(ListNode head) {
        // Initialize a stack to store the values of the linked list
        Stack<Integer> values = new Stack<>();
        int val = 0;

        // Traverse the linked list and push its values onto the stack
        while (head != null) {
            values.push(head.val);
            head = head.next;
        }

        ListNode newTail = null;

        // Iterate over the stack of values and the carryover
        while (!values.isEmpty() || val != 0) {
            // Create a new ListNode with value 0 and the previous tail as its next node
            newTail = new ListNode(0, newTail);

            // Calculate the new value for the current node
            // by doubling the last digit, adding carry, and getting the remainder
            if (!values.isEmpty()) {
                val += values.pop() * 2;
            }
            newTail.val = val % 10;
            val /= 10;
        }

        // Return the tail of the new linked list
        return newTail;
    }
}
```
---
## Solution (Recursion)
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
    // To compute twice the value of each node's value and propagate carry
    public int twiceOfVal(ListNode head) {
        // Base case: if head is null, return 0
        if (head == null) return 0;
        
        // Double the value of current node and add the result of next nodes
        int doubledValue = head.val * 2 + twiceOfVal(head.next);
        
        // Update current node's value with the units digit of the result
        head.val = doubledValue % 10;
        
        // Return the carry (tens digit of the result)
        return doubledValue / 10;
    }
    
    public ListNode doubleIt(ListNode head) {
        int carry = twiceOfVal(head);
        
        // If there's a carry, insert a new node at the beginning with the carry value
        if (carry != 0) {
            head = new ListNode(carry, head);
        }
        
        return head;
    }
}
```
---
## Solution (Two Pointers)
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
    public ListNode doubleIt(ListNode head) {
        ListNode curr = head;
        ListNode prev = null;

        // Traverse the linked list
        while (curr != null) {
            int twiceOfVal = curr.val * 2;

            // If the doubled value is less than 10
            if (twiceOfVal < 10) {
                curr.val = twiceOfVal;
            } 
            // If doubled value is 10 or greater
            else if (prev != null) { // other than first node
                // Update current node's value with units digit of the doubled value
                curr.val = twiceOfVal % 10;
                // Add the carry to the previous node's value
                prev.val = prev.val + 1;
            } 
            // If it's the first node and doubled value is 10 or greater
            else { // first node
                // Create a new node with carry as value and link it to the current node
                head = new ListNode(1, curr);
                // Update current node's value with units digit of the doubled value
                curr.val = twiceOfVal % 10;
            }

            // Update prev and curr pointers
            prev = curr;
            curr = curr.next;
        }
        return head;
    }
}
```
