# 31. Next Permutation

## 1. Theoretical Concepts & Intuition
A permutation is a specific ordering of numbers. The "Next Permutation" is the lexicographically next greater permutation. If no such permutation exists (the array is sorted in descending order), we return the smallest possible permutation (sorted in ascending order).

The core intuition relies on finding the **break-point** where the descending sequence from the right is interrupted.
1. From the right, find the first index $i$ where $A[i] < A[i+1]$. This is our "dip".
2. If no such index exists, the whole array is descending; just reverse it.
3. If it exists, find the smallest number to the right of $i$ that is greater than $A[i]$.
4. Swap them and reverse everything to the right of index $i$ to get the smallest possible tail.


## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force (All Permutations)** | $O(N! \cdot N)$ | $O(N!)$ |
| **STL Function** | $O(N)$ | $O(1)$ |
| **Optimal (Single Pass)** | $O(N)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1: Brute Force** Generate all permutations, sort them, find the current one, and return the next. Extremely slow for large arrays.
* **Approach 2: C++ STL** Use the built-in `std::next_permutation(A.begin(), A.end())` function.
* **Approach 3: Optimal Observation** 1. Find break-point $i$ where $A[i] < A[i+1]$.
    2. Find the smallest element $> A[i]$ from the right and swap.
    3. Reverse the part after index $i$.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>

using std::vector;
using std::reverse;
using std::swap;

class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        // --- APPROACH 2: STL ---
        // std::next_permutation(nums.begin(), nums.end());

        // --- APPROACH 3: OPTIMAL ---
        int n = nums.size();
        int index = -1;

        // Step 1: Find the break-point
        for (int i = n - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                index = i;
                break;
            }
        }

        // If no break-point, reverse whole array
        if (index == -1) {
            reverse(nums.begin(), nums.end());
            return;
        }

        // Step 2: Find next greater element to swap with
        for (int i = n - 1; i > index; i--) {
            if (nums[i] > nums[index]) {
                swap(nums[i], nums[index]);
                break;
            }
        }

        // Step 3: Reverse the remaining part
        reverse(nums.begin() + index + 1, nums.end());
    }
};
