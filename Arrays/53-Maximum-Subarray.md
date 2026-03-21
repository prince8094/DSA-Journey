# 53. Maximum Subarray (Kadane's Algorithm)

## 1. Theoretical Concepts & Intuition
We want to find the contiguous subarray with the largest sum. 

* **Intuition:** If a subarray sum becomes negative, it will only decrease the sum of any future subarray it is part of. Therefore, we reset the current sum to 0 whenever it drops below zero.


## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Kadane's Algo**| $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach (Kadane's):**
    1. `sum = 0`, `maxi = nums[0]`.
    2. For each element: Add to `sum`.
    3. Update `maxi = max(sum, maxi)`.
    4. If `sum < 0`, reset `sum = 0`.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>

using std::vector;
using std::max;

class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int sum = 0;
        int maxi = nums[0];

        for (int num : nums) {
            sum += num;
            maxi = max(sum, maxi);
            if (sum < 0) {
                sum = 0; // **Reset if sum becomes a burden**
            }
        }
        return maxi;
    }
};
