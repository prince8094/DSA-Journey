# Linked List End Insertion

## 1. Theoretical Concepts & Intuition
Inserting a node at the end (tail) of a singly linked list requires finding the current last node. The last node is distinctly identified because its `next` pointer evaluates to `nullptr`. 

*   **Edge Case:** If the given list is entirely empty (`head == nullptr`), the new node itself becomes the `head` of the list.
*   **Traversal:** We use a temporary pointer to walk through the list until we hit the condition `temp->next == nullptr`. We then update this pointer to point to our newly created node.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Linear Traversal** | $O(N)$ | $O(1)$ |

## 3. Summary of all Approaches
*   **Approach 1 (Traversal to Tail):**
    1. Create a `newptr` node with the given value `x`.
    2. If `head` is `nullptr`, return `newptr` as the new head.
    3. Set a `temp` pointer to `head`.
    4. Traverse using `while(temp->next != nullptr)` to reach the last node.
    5. Point `temp->next` to `newptr`.
    6. Ensure `newptr->next` is `nullptr`.
    7. Return the unmodified `head`.

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
    Node *insertAtEnd(Node *head, int x) {
        Node* newptr = new Node(x);
        
        // Edge case: empty list
        if(head == nullptr) return newptr;
        
        Node* temp = head;
        // Traverse to the last node
        while(temp->next != nullptr){
            temp = temp->next;
        }
        
        // Link the new node at the end
        temp->next = newptr;
        newptr->next = nullptr;
        
        return head;
    }
};
