# 485. Max Consecutive Ones

## 1. Theoretical Concepts & Intuition
We need to find the maximum number of consecutive $1$s in a binary array. 
The logic is to keep a running counter. Every time we see a $1$, we increment it and update our maximum. Every time we see a $0$, we reset the counter.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Single Pass** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach:**
    1. Initialize `count = 0` and `maxi = 0`.
    2. Iterate through the array.
    3. If $arr[i] == 1$, `count++`.
    4. Update `maxi = max(maxi, count)`.
    5. If $arr[i] == 0$, reset `count = 0`.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>

using std::vector;
using std::max;

class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int count = 0;
        int maxi = 0;
        
        for (int num : nums) {
            if (num == 1) {
                count++;
                maxi = max(maxi, count); // **Track highest count**
            } else {
                count = 0; // **Reset on zero**
            }
        }
        return maxi;
    }
};
