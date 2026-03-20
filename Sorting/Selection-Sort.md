
# Selection Sort

## 1. Theoretical Concepts & Intuition
Selection sort works by repeatedly finding the minimum element from the unsorted part of the array and putting it at the beginning. 
For an array of size $n$, we perform $n-1$ passes. In each pass $i$, we find the smallest element in the range $[i, n-1]$ and swap it with the element at index $i$.

## 2. Time/Space Complexity Table
| Scenario | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **All Cases** | $O(n^2)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Selection Algorithm:**
    1. Outer loop runs from $i = 0$ to $n-2$.
    2. Assume $i$ is the index of the minimum element (`mini = i`).
    3. Inner loop finds the actual minimum in the remaining unsorted part.
    4. Swap the found minimum with the element at $i$.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>

using std::vector;
using std::swap;

void selectionSort(vector<int>& arr, int n) {
    for (int i = 0; i <= n - 2; i++) {
        int mini = i; // Assume current is min
        for (int j = i; j < n; j++) {
            if (arr[j] < arr[mini]) {
                mini = j; // **Found a new minimum**
            }
        }
        swap(arr[i], arr[mini]); // **Swap min to current position**
    }
}

---
