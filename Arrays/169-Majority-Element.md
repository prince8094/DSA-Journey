# 169. Majority Element

## 1. Theoretical Concepts & Intuition
A majority element appears more than $\lfloor n/2 \rfloor$ times. 

* **Sorting Intuition:** If an element appears more than half the time, it must occupy the middle index ($n/2$) when the array is sorted.
* **Boyer-Moore Voting:** This is the most efficient. We maintain a "candidate" and a "count". If the next element is the same as the candidate, `count++`; otherwise, `count--`.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Sorting** | $O(n \log n)$ | $O(1)$ |
| **Hashing** | $O(n)$ | $O(n)$ |
| **Boyer-Moore**| $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Sorting):** Sort and return `nums[n/2]`.
* **Approach 2 (Hashing):** Use a map to store frequencies. Return the element where `map[val] > n/2`.
* **Approach 3 (Boyer-Moore):** 1. Start with `count = 0`. 2. If `count == 0`, set candidate to current element. 3. If element matches candidate, `count++`, else `count--`.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count = 0;
        int element = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (count == 0) {
                element = nums[i];
                count = 1;
            } else if (nums[i] == element) {
                count++;
            } else {
                count--;
            }
        }
        
        // Manual verification check could be added here if needed
        return element;
    }
};
