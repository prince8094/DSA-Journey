# 3783. Mirror Distance of an Integer

## 1. Theoretical Concepts & Intuition
The "Mirror Distance" is defined as $|n - reverse(n)|$. 

* **Reversing Logic:** To reverse a number, we repeatedly take the last digit (`n % 10`) and append it to a new variable (`rev * 10 + digit`).
* **Absolute Value:** Since the distance must be non-negative, we use the `abs()` function.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Mathematical Reversal** | $O(\log_{10} n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Helper Function):** 1. Define a `reverse` function that extracts digits and reconstructs them in reverse order.
    2. Call this function in `mirrorDistance`.
    3. Return the absolute difference between the original and reversed value.

## 4. Full C++ Code implementations
```cpp
#include <cmath>

using std::abs;

class Solution {
public:
    int reverse(int n) {
        int rev = 0;
        while(n > 0) {
            int rem = n % 10;
            rev = rev * 10 + rem;
            n = n / 10;
        }
        return rev;
    }
    
    int mirrorDistance(int n) {
        return abs(n - reverse(n));
    }
};
