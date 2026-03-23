# 2535. Difference Between Element Sum and Digit Sum of an Array

## 1. Theoretical Concepts & Intuition
We need to find the absolute difference between two values:
1.  **Element Sum:** The total of all raw numbers in the array.
2.  **Digit Sum:** The total of every individual digit of every number in the array.

Example: For `[15, 3]`, Element Sum = $15+3=18$, Digit Sum = $1+5+3=9$. Difference = $|18-9| = 9$.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Single Pass** | $O(n \cdot \text{digits})$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Simultaneous Summing):** 1. Loop through the array.
    2. Add the whole number to `sum`.
    3. Use a nested `while` loop to break the number down into digits and add them to `dsum`.
    4. Return the absolute difference using `abs()`.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <cmath>

using std::vector;
using std::abs;

class Solution {
public:
    int differenceOfSum(vector<int>& nums) {
        int sum = 0;
        int dsum = 0;
        
        for(int i = 0; i < nums.size(); i++) {
            sum += nums[i]; // Calculate Element Sum
            
            int temp = nums[i];
            while(temp > 0) {
                int rem = temp % 10;
                dsum += rem; // Calculate Digit Sum
                temp /= 10;
            }
        }
        return abs(dsum - sum);
    }
};
