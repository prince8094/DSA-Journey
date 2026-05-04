# 232. Implement Queue using Stacks

## 1. Theoretical Concepts & Intuition
A **Queue** requires FIFO order, but a **Stack** reverses order (LIFO). 
* **The Double Reversal Trick:** If you push elements into one stack, their order is reversed. If you then pop them from that stack and push them into a second stack, the order is reversed *again*. Reversing a reversed order restores the original FIFO order.
* **Two Strategies:**
    1.  **Push-Heavy:** Make the `push` operation do the heavy lifting ($O(N)$) so `pop` is instant.
    2.  **Pop-Heavy (Amortized):** Push elements quickly ($O(1)$) and only transfer elements between stacks during a `pop` when necessary. This provides an amortized $O(1)$ time for popping.



## 2. Time/Space Complexity Table
| Approach | Push Time | Pop Time | Space Complexity |
| :--- | :--- | :--- | :--- |
| **Push-Heavy (Making Push O(N))** | $O(N)$ | $O(1)$ | $O(N)$ |
| **Pop-Heavy (Amortized)** | $O(1)$ | Amortized $O(1)$ | $O(N)$ |

## 3. Summary of all Approaches
* **Approach 1 (Push-Heavy):** To push, move everything from `s1` to `s2`. Push the new element to `s1`. Move everything back from `s2` to `s1`. The oldest element is always safely at the top of `s1`.
* **Approach 2 (Pop-Heavy / Optimal):** 
    1.  **Push:** Always push into `s1`.
    2.  **Pop:** If `s2` is empty, pour everything from `s1` into `s2`. This flips the order. The top of `s2` is now the queue's front. Pop it. Future pops will be $O(1)$ as long as `s2` isn't empty.

## 4. Full C++ Code implementations
```cpp
#include <stack>

using std::stack;

class StackQueue {
private:
    stack<int> s1; // Input stack
    stack<int> s2; // Output stack
public:
    void push(int B);
    int pop();
};

void StackQueue::push(int B) {
    // --- APPROACH 1: PUSH HEAVY O(N) ---
    /*
    while(!s1.empty()){
        s2.push(s1.top());
        s1.pop();
    }
    s1.push(B);
    while(!s2.empty()){
        s1.push(s2.top());
        s2.pop();
    }
    */

    // --- APPROACH 2: POP HEAVY / OPTIMAL O(1) ---
    s1.push(B);
}

int StackQueue::pop() {
    // --- APPROACH 1: PUSH HEAVY O(1) ---
    /*
    if(s1.empty()){
        return -1; 
    }
    int x = s1.top();
    s1.pop();
    return x;
    */

    // --- APPROACH 2: POP HEAVY / OPTIMAL Amortized O(1) ---
    if(s1.empty() && s2.empty()) {
        return -1;
    }
    
    // If output stack is empty, pour s1 into s2 to reverse order
    if(s2.empty()) {
        while(!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
    }
    
    int x = s2.top();
    s2.pop();
    return x;
}
