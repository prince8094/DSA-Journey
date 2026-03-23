# 3876. Construct Uniform Parity Array II

## 1. Theoretical Concepts & Intuition
The problem involves deciding if we can transform an array into one that is **all even** or **all odd**. We are allowed to subtract $nums1[j]$ from $nums1[i]$ to achieve this.

* **Key Insight:** To make an array all even, every element $nums1[i]$ must be $\ge$ the smallest even number or we must be able to subtract an odd number from an odd element to make it even. 
* **Crucial Logic:** The simplest way to satisfy the parity for all indices is by comparing the minimum odd and minimum even values. If an entire parity is missing, it's trivial. Otherwise, the relationship between `minOdd` and `minEven` determines the feasibility.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Minimum Tracking** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Min-Parity Comparison):** 1. Traverse the array once to find the minimum odd value and minimum even value.
    2. If all numbers are already the same parity (either `minOdd` or `minEven` remains `INT_MAX`), return `true`.
    3. Compare `minOdd` and `minEven`. If `minOdd < minEven`, we can use the odd number to transform others.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>
#include <climits>

using std::vector;
using std::min;

class Solution {
public:
    bool uniformArray(vector<int>& nums1) {
        int minOdd = INT_MAX;
        int minEven = INT_MAX;
        
        for(int x : nums1) {
            if(x % 2 != 0) minOdd = min(minOdd, x);
            else minEven = min(minEven, x);
        }
        
        // If one parity is completely missing, array is already uniform
        if(minOdd == INT_MAX || minEven == INT_MAX) {
            return true;
        }
        
        // Logic based on the smallest odd number's ability to change parity
        return minOdd < minEven;
    }
};
