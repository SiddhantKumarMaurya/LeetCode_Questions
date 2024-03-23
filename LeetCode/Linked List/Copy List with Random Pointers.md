# [Copy List with Random Pointers](https://leetcode.com/problems/copy-list-with-random-pointer/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/a9aaf9a7-73a2-47b0-9a36-df190a84a13d)
## 
```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;

        // create new nodes and insert them between the original nodes
        Node current = head;
        while (current != null) {
            Node newNode = new Node(current.val);
            newNode.next = current.next;
            current.next = newNode;
            current = newNode.next;
        }

        // Assign random pointers for new nodes
        current  = head;
        while (current != null) {
            if (current.random != null) {
                current.next.random = current.random.next;
            }
            current = current.next.next;
        }

        // Seperate original list from the copied list;
        current = head;
        Node newHead = head.next;
        Node newCurrent = newHead;

        while (current != null) {
            current.next = current.next.next;
            if (newCurrent.next != null) {
                newCurrent.next = newCurrent.next.next;
            }
            current = current.next;
            newCurrent = newCurrent.next;
        }
        return newHead;
    }
}
```
