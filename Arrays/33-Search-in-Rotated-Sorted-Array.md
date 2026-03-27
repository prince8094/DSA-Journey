# 33. Search in Rotated Sorted Array

## 1. Theoretical Concepts & Intuition
A rotated sorted array (e.g., `[4,5,6,7,0,1,2]`) is no longer fully sorted, but it remains **locally sorted**. 

* **The Key Property:** At any given `mid` index, either the left half `[low...mid]` or the right half `[mid...high]` **must** be sorted.
* **Decision Making:** We identify which half is sorted. If the target lies within the range of that sorted half, we discard the other half. Otherwise, we search in the unsorted half.



## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Modified Binary Search** | $O(\log N)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Optimized B.S.):** 1. If `nums[low] <= nums[mid]`, the left side is sorted.
        - Check if target is between `nums[low]` and `nums[mid]`.
    2. Else, the right side is sorted.
        - Check if target is between `nums[mid]` and `nums[high]`.
    3. Shrink the search space based on these checks.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    int search(vector<int>& nums, int target) {
        int low = 0, high = nums.size() - 1;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) return mid;

            // Check if left part is sorted
            if (nums[low] <= nums[mid]) {
                if (target >= nums[low] && target < nums[mid]) high = mid - 1;
                else low = mid + 1;
            } 
            // Right part must be sorted
            else {
                if (target > nums[mid] && target <= nums[high]) low = mid + 1;
                else high = mid - 1;
            }
        }
        return -1;
    }
};
