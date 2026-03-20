# 26. Remove Duplicates from Sorted Array

## 1. Theoretical Concepts & Intuition
The problem provides a sorted array and requires us to remove duplicates in-place such that each unique element appears only once. Since the array is sorted, all duplicate elements will be adjacent.

The intuition is to keep track of a "unique" boundary. We use a pointer ($k$) to mark the position where the next unique element should be placed. As we iterate through the array, we only move an element to the $k^{th}$ position if it is different from the previously recorded unique element.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Two Pointers** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Two-Pointer Approach:** 1. Initialize a pointer $k = 1$ (since the first element is always unique).
    2. Iterate from $i = 1$ to $n-1$.
    3. If $arr[i] \neq arr[i-1]$, it is a new unique element.
    4. Move it to $arr[k]$ and increment $k$.
    5. Return $k$ as the count of unique elements.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0;
        
        int k = 1; // Index for the next unique element
        for (int i = 1; i < nums.size(); i++) {
            // Check if current element is different from previous
            if (nums[i] != nums[i - 1]) {
                nums[k] = nums[i]; // **Place unique element at index k**
                k++;
            }
        }
        return k;
    }
};
