# LinkedList Traversal

## 1. Theoretical Concepts & Intuition
Traversal is the process of visiting every node in a data structure exactly once. In a singly linked list, we must traverse sequentially starting strictly from the `head`.

We use a temporary pointer that moves from node to node using the `next` references until the pointer becomes `nullptr`, which signifies that we have walked past the final node in the list.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Linear Iteration** | $O(N)$ | $O(1)$ |

## 3. Summary of all Approaches
*   **Approach 1 (While Loop Iteration):**
    1. Initialize a `temp` pointer pointing to the `head`.
    2. Initiate a `while` loop that continues as long as `temp != nullptr`.
    3. Print `temp->data`.
    4. Advance the pointer to the next node (`temp = temp->next`).

## 4. Full C++ Code implementations
```cpp
#include <iostream>

using std::cout;

/*
class Node {
public:
    int data;
    Node* next;
    Node(int val) {
        data = val;
        next = nullptr;
    }
};
*/

class Solution {
public:
    void printList(Node* head) {
        Node* temp = head;
        
        // Iterate until the end of the list is reached
        while(temp != nullptr){
            cout << temp->data << " ";
            temp = temp->next; // Advance to next node
        }
    }
};
