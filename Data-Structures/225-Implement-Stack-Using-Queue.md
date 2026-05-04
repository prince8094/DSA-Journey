# 225. Implement Stack using Queue

## 1. Theoretical Concepts & Intuition
A **Stack** follows the Last-In-First-Out (LIFO) principle, while a **Queue** follows First-In-First-Out (FIFO). To make a queue behave like a stack, the most recently added element must always be at the front of the queue.

* **Single Queue Rotation:** When a new element is added to the rear of the queue, it's in the wrong position for a stack (it should be at the front). We can fix this by taking all the elements that were in the queue *before* the new element and rotating them.
* **The Rotation Process:** We dequeue the front elements and immediately enqueue them back to the rear. After doing this exactly $size - 1$ times, the newly added element naturally becomes the new front of the queue.



## 2. Time/Space Complexity Table
| Operation | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Push** | $O(N)$ | $O(N)$ (Queue storage) |
| **Pop** | $O(1)$ | $O(1)$ auxiliary |
| **Top** | $O(1)$ | $O(1)$ auxiliary |

## 3. Summary of all Approaches
* **Approach (Single Queue Rotation):**
    1.  **Push:** Record the current size $S$ of the queue. Push the new element $x$. Run a loop $S$ times where you extract the front element (`q.front()`) and push it back to the rear (`q.push()`), then `q.pop()`.
    2.  **Pop:** Since the queue is always perfectly ordered like a stack, simply `pop()` the front element.
    3.  **Top:** Return `q.front()`.

## 4. Full C++ Code implementations
```cpp
#include <queue>

using std::queue;

class myStack {
    queue<int> q;

public:
    void push(int x) {
        // Inserts an element x at the top of the stack
        int s = q.size();
        q.push(x);
        
        // Rotate the previous elements behind the newly added element
        for(int i = 1; i <= s; i++) {
            q.push(q.front());
            q.pop();
        }
    }

    void pop() {
        // Removes an element from the top of the stack
        if(!q.empty()) {
            q.pop();
        }
    }

    int top() {
        // Returns the top element of the stack
        if(q.empty()) return -1;
        return q.front();
    }

    int size() {
        // Returns the current size of the stack
        return q.size();
    }
};
