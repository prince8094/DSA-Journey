# Stack Implementation (Array Based)

## 1. Theoretical Concepts & Intuition
A **Stack** is a linear data structure that follows the Last-In-First-Out (LIFO) principle. You can think of it like a stack of plates: the last plate you put on top is the first one you take off.

* **Top Pointer:** We only need a single pointer/index called `top` to keep track of the most recently added element. 
* Unlike a queue, a stack naturally reuses its allocated array space as elements are popped and pushed, so no circular logic is required. It only becomes full when the `top` index reaches $size - 1$.

## 2. Time/Space Complexity Table
| Operation | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Push** | $O(1)$ | $O(1)$ |
| **Pop** | $O(1)$ | $O(1)$ |
| **Peek** | $O(1)$ | $O(1)$ |
| **Overall Structure** | - | $O(n)$ |

## 3. Summary of all Approaches
* **Array-Based Approach:**
    1.  Maintain a `top` pointer initialized to `-1`.
    2.  **isEmpty:** True if $top == -1$.
    3.  **isFull:** True if $top == size - 1$.
    4.  **Push:** Increment `top` by $1$ and place the new element at `arr[top]`.
    5.  **Pop:** Decrement `top` by $1$ (the element remains in memory but is "logically" removed since `top` has shifted down).
    6.  **Peek:** Return `arr[top]`.

## 4. Full C++ Code implementations
```cpp
#include <iostream>

using namespace std;

class myStack {
    int top;
    int* arr;
    int size;

public:
    myStack(int n) {
        top = -1;
        size = n;
        arr = new int[n];
    }

    ~myStack() {
        delete[] arr; // Free dynamically allocated memory
    }

    bool isEmpty() {
        return top == -1;
    }

    bool isFull() {
        return top == size - 1;
    }

    void push(int x) {
        if (isFull()) {
            return;
        }
        top++;
        arr[top] = x;
    }

    void pop() {
        if (isEmpty()) {
            return;
        }
        top--;
    }

    int peek() {
        if (isEmpty()) {
            return -1;
        }
        return arr[top];
    }
};
