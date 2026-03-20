# 283. Move Zeroes

## 1. Theoretical Concepts & Intuition
The task is to move all zeroes to the end while maintaining the relative order of non-zero elements. 

* **Brute Force:** Copy non-zeroes to a new array, then fill the rest with zeroes.
* **Optimized (Two Pointers):** Find the first zero, then iterate and swap any non-zero element with that zero position.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(n)$ | $O(n)$ |
| **Optimal (Swap)** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1: Temp Array** Create a new array, fill non-zeroes, then copy back.
* **Approach 2: Two-Pointer Swap**
    1. Find the index $j$ of the first zero.
    2. If no zero is found, return.
    3. Iterate from $i = j+1$ to $n-1$.
    4. If $arr[i] \neq 0$, swap $arr[i]$ with $arr[j]$ and increment $j$.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>

using std::vector;
using std::swap;

class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        int j = -1;
        
        // Find first zero
        for (int i = 0; i < n; i++) {
            if (nums[i] == 0) {
                j = i;
                break;
                   }
        }
        
        // No zeroes found
        if (j == -1) return;
        
        // Swap non-zeroes with the pointer j
        for (int i = j + 1; i < n; i++) {
            if (nums[i] != 0) {
                swap(nums[i], nums[j]);
                j++; // **j always points to a zero after swap**
            }
        }
    }
};
