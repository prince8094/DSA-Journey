# 35. Search Insert Position

## 1. Theoretical Concepts & Intuition
The problem asks for the index of a target in a sorted array, or the index where it should be inserted to maintain order.

* **Binary Search Logic:** Since the array is sorted, we use two pointers (`low` and `high`).
* **The "Lower Bound" Concept:** If the target is not found, the `low` pointer will eventually cross `high` and land exactly at the index where the target should be inserted. This is because `low` always moves to the first element that is greater than the target when the search fails.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Binary Search** | $O(\log N)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Optimal Binary Search):** 1. Initialize `low = 0` and `high = n - 1`.
    2. While `low <= high`:
        - Calculate `mid`.
        - If `nums[mid] == target`, return `mid`.
        - If `nums[mid] < target`, move `low = mid + 1`.
        - Else, move `high = mid - 1`.
    3. If the loop finishes, `low` is the insertion index.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int low = 0, high = nums.size() - 1;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) low = mid + 1;
            else high = mid - 1;
        }
        return low; // **Start node: index where it would be found if present**
    }
};
