# Copy a Linked List with Random Pointer
## https://leetcode.com/problems/copy-list-with-random-pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

The Linked List is represented in the input/output as a list of n nodes. Each node is represented as a pair of [val, random_index] where:

val: an integer representing Node.val
random_index: the index of the node (range from 0 to n-1) where random pointer points to, or null if it does not point to any node.

## Implementation 1 : O(n)

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
        if (head == null)
            return null;
        Map<Node, Node> cloneMap = new HashMap<>();
        Node curr = head;
        while (curr != null) {
          cloneMap.put(curr, new Node(curr.val));
          curr = curr.next;
        }
        
        curr = head;
        while (curr != null) {
            cloneMap.get(curr).next = cloneMap.get(curr.next);
            cloneMap.get(curr).random = cloneMap.get(curr.random);
            curr = curr.next;
        }
        return cloneMap.get(head);
    }
}

```

## Implementation 2 : O(1)

# References :
https://www.youtube.com/watch?v=OvpKeraoxW0
