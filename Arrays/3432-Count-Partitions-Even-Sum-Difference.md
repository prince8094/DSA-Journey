# 3432. Count Partitions with Even Sum Difference

## 1. Theoretical Concepts & Intuition
A "partition" splits an array into a non-empty **Left Subarray** and a **Right Subarray**. We need to count partitions where $(RightSum - LeftSum)$ is even.

* **Mathematical Trick:** The difference between two numbers $(A - B)$ has the same parity (even/odd) as their sum $(A + B)$. Since $(RightSum + LeftSum) = TotalSum$, the difference is even if the `TotalSum` and $2 \cdot LeftSum$ share parity properties.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Prefix Sum/Running Sum** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Two Pass):** 1. First pass: Calculate the total sum of the array (`rsum`).
    2. Second pass: Iterate from $0$ to $n-2$ (to ensure right subarray is non-empty).
    3. Move the current element from `rsum` to `lsum`.
    4. Check if `(rsum - lsum) % 2 == 0`.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    int countPartitions(vector<int>& nums) {
        int lsum = 0;
        int rsum = 0;
        int count = 0;
        
        // Initial total sum stored in rsum
        for(int i = 0; i < nums.size(); i++) {
            rsum += nums[i];
        }
        
        // Partitioning: i goes to nums.size() - 1 to leave at least one element on the right
        for(int i = 0; i < nums.size() - 1; i++) {
            lsum += nums[i];
            rsum -= nums[i];
            
            if((rsum - lsum) % 2 == 0) {
                count++;
            }
        }
        return count;
    }
};
