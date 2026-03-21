# 1. Two Sum

## 1. Theoretical Concepts & Intuition
The goal is to find indices of two numbers in an array that add up to a specific target. 

* **Brute Force Logic:** For every element at index $i$, we scan the rest of the array (indices $j > i$) to see if $nums[i] + nums[j] == target$.
* **Key Idea:** Every number $x$ is looking for its partner $y$ such that $y = target - x$.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(n^2)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Brute Force):** 1. Iterate with index $i$ from $0$ to $n-1$.
    2. Start a second loop with index $j = i+1$.
    3. If the sum equals the target, return $\{i, j\}$.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        for (int i = 0; i < n; i++) {
            int j = i + 1;
            while (j < n) {
                if (nums[i] + nums[j] == target) {
                    return {i, j};
                }
                j++;
            }
        }
        return {};
    }
};
