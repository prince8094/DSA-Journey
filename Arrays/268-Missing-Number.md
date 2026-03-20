# 268. Missing Number

## 1. Theoretical Concepts & Intuition
Given an array containing $n$ distinct numbers in the range $[0, n]$, find the one that is missing.
The most efficient way uses the mathematical formula for the sum of the first $n$ natural numbers: $Sum = \frac{n(n+1)}{2}$.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Sorting** | $O(n \log n)$ | $O(1)$ |
| **Sum Formula** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1: Sorting** Sort the array and check if $arr[i] \neq i$.
* **Approach 2: Mathematical Sum** 1. Calculate the expected sum $S1 = \frac{n(n+1)}{2}$.
    2. Calculate the actual sum $S2$ of all elements in the array.
    3. The missing number is $S1 - S2$.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <numeric>

using std::vector;

class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        
        // Expected sum of numbers from 0 to n
        int expectedSum = (n * (n + 1)) / 2;
        
        int actualSum = 0;
        for (int num : nums) {
            actualSum += num;
        }
        
        return expectedSum - actualSum;
    }
};
