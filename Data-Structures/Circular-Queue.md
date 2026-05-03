# Circular Queue Implementation (Array Based)

## 1. Theoretical Concepts & Intuition
A **Queue** is a linear data structure that operates on the First-In-First-Out (FIFO) principle. Elements are inserted at the `rear` and removed from the `front`. 

* **The Problem with Standard Array Queues:** In a standard array-based queue, as we `enqueue` and `dequeue` elements, the `front` and `rear` pointers continuously move forward. Eventually, the `rear` reaches the end of the array, but there might be empty spaces at the beginning (because of previous dequeues). 
* **The Circular Queue Solution:** A circular queue connects the end of the array back to the beginning, forming a circle. We achieve this mathematically using the modulo operator.
    * **Wrap-around formula:** $next\_index = (current\_index + 1) \pmod{size}$
    * This ensures that if $current\_index == size - 1$, the next index wraps cleanly to $0$, utilizing all available space perfectly.

## 2. Time/Space Complexity Table
| Operation | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Enqueue** | $O(1)$ | $O(1)$ |
| **Dequeue** | $O(1)$ | $O(1)$ |
| **getFront / getRear** | $O(1)$ | $O(1)$ |
| **Overall Structure** | - | $O(n)$ |

## 3. Summary of all Approaches
* **Array-Based Circular Approach:**
    1.  Maintain two pointers, `front` and `rear`, both initialized to `-1`.
    2.  **isEmpty:** True if $front == -1$.
    3.  **isFull:** True if the next position of `rear` hits `front`, mathematically evaluated as $(rear + 1) \pmod{size} == front$.
    4.  **Enqueue:** If not full, advance `rear` circularly and insert. If it was the first element, set both `front` and `rear` to $0$.
    5.  **Dequeue:** If not empty, advance `front` circularly. If it was the last element, reset both pointers to `-1`.

## 4. Full C++ Code implementations
```cpp
#include <iostream>

using namespace std;

class myQueue {
    int front;
    int rear;
    int *arr;
    int size;

public:
    myQueue(int n) {
        // Define Data Structures
        size = n;
        arr = new int[n];
        front = -1;
        rear = -1;
    }

    ~myQueue() {
        delete[] arr; // Free dynamically allocated memory
    }

    bool isEmpty() {
        // check if the queue is empty
        return front == -1;
    }

    bool isFull() {
        // check if the queue is full
        return ((rear + 1) % size == front);
    }

    void enqueue(int x) {
        // Adds an element x at the rear of the queue.
        if(isFull())
            return;
            
        if(isEmpty()){
            rear = front = 0;
        } else {
            rear = (rear + 1) % size;
        }
        arr[rear] = x;
    }

    void dequeue() {
        // Removes the front element of the queue.
        if(isEmpty()) return;
        
        if(front == rear){
            // Queue becomes empty after this dequeue
            front = rear = -1;
        } else {
            front = (front + 1) % size;
        }
    }

    int getFront() {
        // Returns the front element of the queue.
        if(isEmpty()) return -1;
        return arr[front];
    }

    int getRear() {
        // Return the last element of queue
        if(isEmpty()) return -1;
        return arr[rear];
    }
};
