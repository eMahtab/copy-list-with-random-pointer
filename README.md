# Copy a Linked List with Random Pointer
## https://leetcode.com/problems/copy-list-with-random-pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

The Linked List is represented in the input/output as a list of n nodes. Each node is represented as a pair of [val, random_index] where:

val: an integer representing Node.val
random_index: the index of the node (range from 0 to n-1) where random pointer points to, or null if it does not point to any node.

## From the past :
Well, we already know how to clone a linked list. 
Just iterate through the linked list, create new node and connect the previous node with the current node, and update the pointers.

```java
public ListNode clone(ListNode head) {
     ListNode prev = null, copyHead = null, ptr = head;
     while(ptr != null) {
	ListNode node = new ListNode(ptr.val);
	if(prev == null) 
	   copyHead = node;
	if(prev != null) {
	   prev.next = node;
	}
	prev = node;
	ptr = ptr.next;
     }
   return copyHead;
}
```
But wait, this problem have an extra level of complexity. In this list each node have a random pointer, which may point to a node forward in the list.
So we better first create all the nodes (in the first iteration) and in the second iteration just connect the next and random pointer correctly.


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
      Node curr = head;
      Node next = null;
        
      while (curr != null) {
       Node copy = new Node(curr.val);     
       next = curr.next;
       curr.next = copy;
       copy.next = next;
       curr = next;
      }
        
      curr = head;
      while (curr != null) {
          if (curr.random != null) { 
            curr.next.random = curr.random.next;
          }
          curr = curr.next.next;    
      }
        
      curr = head;
      Node cloneListHead = curr.next; 
        
      while(curr != null){
          next = curr.next.next;
          Node cloneNode = curr.next;
          cloneNode.next = (next != null) ? next.next : null;
          curr.next = next;
          curr = next;
      }  
      return cloneListHead;   
   }
}
```

💥 ❗️  Caution : NullPointerException

# References :
1. https://www.youtube.com/watch?v=OvpKeraoxW0
2. https://github.com/bephrem1/backtobackswe/tree/master/Linked%20Lists/CloneLinkedListWithRandomPointers
3. https://leetcode.com/articles/copy-list-with-random-pointer
