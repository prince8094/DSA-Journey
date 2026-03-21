# 75. Sort Colors

## 1. Theoretical Concepts & Intuition
This is the **Dutch National Flag algorithm**. We need to sort an array containing only 0s, 1s, and 2s in-place.

* **Counting Method:** Count 0s, 1s, and 2s, then rewrite the array.
* **Three-Pointer Method:** Maintain three zones: $[0 \dots low-1]$ for 0s, $[low \dots mid-1]$ for 1s, and $[high+1 \dots n-1]$ for 2s.


## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Counting Sort** | $O(n)$ | $O(1)$ |
| **DNF Algorithm** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Counting):** Use fake counters for 0, 1, and 2. Then replace array values with 0s until `cnt0`, 1s until `cnt0+cnt1`, etc.
* **Approach 2 (DNF):** 1. $s = 0, mid = 0, e = n-1$.
    2. If $nums[mid] == 0$: Swap with $nums[s]$, increment $s$ and $mid$.
    3. If $nums[mid] == 1$: Just increment $mid$.
    4. If $nums[mid] == 2$: Swap with $nums[e]$, decrement $e$.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>

using std::vector;
using std::swap;

class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = nums.size();
        int s = 0, mid = 0, e = n - 1;

        while (mid <= e) {
            if (nums[mid] == 0) {
                swap(nums[mid], nums[s]);
                mid++;
                s++;
            } 
            else if (nums[mid] == 1) {
                mid++;
            } 
            else { // nums[mid] == 2
                swap(nums[mid], nums[e]);
                e--;
            }
        }
    }
};
