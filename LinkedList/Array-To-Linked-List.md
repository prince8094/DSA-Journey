# Array to Linked List

## 1. Theoretical Concepts & Intuition
The objective is to convert a given array of integers into a Singly Linked List. A linked list consists of nodes where each node holds a `data` value and a `next` pointer to the subsequent node.

*   **Initialization:** We create the `head` node using the first element of the array.
*   **Sequential Linking:** We use a `mover` pointer (or iterator) that keeps track of the last node in our growing linked list. As we iterate through the remaining elements of the array, we create a new node for each element and link the `mover`'s next pointer to this newly created node.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Iterative Construction** | $O(N)$ | $O(N)$ |

*Note: The space complexity is $O(N)$ because we are allocating heap memory for $N$ new nodes to construct the linked list.*

## 3. Summary of all Approaches
*   **Approach 1 (Iterative Construction):**
    1. Initialize a `head` node with `arr[0]`.
    2. Maintain a `mover` pointer initialized to `head`.
    3. Loop from index $i = 1$ to $arr.size() - 1$.
    4. Inside the loop, instantiate a `temp` node with `arr[i]`.
    5. Link the current list to the new node (`mover->next = temp`).
    6. Advance the `mover` pointer (`mover = mover->next`).
    7. Return the `head` of the constructed list.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

/*
class Node {
public:
    int data;
    Node* next;
    Node(int d) {
        data = d;
        next = nullptr;
    }
};
*/

class Solution {
public:
    Node* arrayToList(vector<int>& arr) {
        // Step 1: Initialize head with the first element
        Node* head = new Node(arr[0]);
        Node* mover = head;
        
        // Step 2: Iterate through the rest of the array
        for(int i = 1; i < arr.size(); i++){
            Node* temp = new Node(arr[i]);
            mover->next = temp;      // Link the new node
            mover = mover->next;     // Move the pointer forward
        }
        
        return head;
    }
};
