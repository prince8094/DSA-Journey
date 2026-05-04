# Linked List Insertion At Beginning

## 1. Theoretical Concepts & Intuition
Inserting a node at the beginning (head) of a linked list is the most efficient insertion operation because it requires no traversal.

We simply construct a new node, point its `next` reference to the *current* `head` of the list, and then update the `head` reference to point to our newly created node.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Pointer Reassignment** | $O(1)$ | $O(1)$ |

## 3. Summary of all Approaches
*   **Approach 1 (Direct Pointer Update):**
    1. Create a `newptr` node with the value `x`.
    2. Assign the `next` pointer of `newptr` to the existing `head`.
    3. Update the `head` pointer to point to `newptr`.
    4. Return the new `head`.

## 4. Full C++ Code implementations
```cpp
/*
class Node {
public:
    int data;
    Node* next;
    Node(int x) {
        data = x;
        next = nullptr;
    }
};
*/

class Solution {
public:
    Node *insertAtFront(Node *head, int x) {
        Node* newptr = new Node(x);
        
        // Point new node to the current head
        newptr->next = head;
        
        // The new node becomes the new head
        head = newptr;
        
        return head;
    }
};
