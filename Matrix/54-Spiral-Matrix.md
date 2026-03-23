# 54. Spiral Matrix

## 1. Theoretical Concepts & Intuition
The goal is to return all elements of a matrix in spiral order (Right $\rightarrow$ Down $\rightarrow$ Left $\rightarrow$ Up). 

The intuition is to maintain four boundaries: `top`, `bottom`, `left`, and `right`. As we finish a row or column, we "shrink" the boundary inward until the boundaries cross each other.


## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Boundary Shrinking** | $O(N \times M)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach:** Use a `while` loop that continues as long as `top <= bottom` and `left <= right`.
    1. **Left to Right:** Traverse `top` row, then `top++`.
    2. **Top to Bottom:** Traverse `right` column, then `right--`.
    3. **Right to Left:** Traverse `bottom` row (check `top <= bottom` first), then `bottom--`.
    4. **Bottom to Top:** Traverse `left` column (check `left <= right` first), then `left++`.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        int top = 0, bottom = n - 1;
        int left = 0, right = m - 1;
        vector<int> ans;

        while (top <= bottom && left <= right) {
            // Left to Right
            for (int i = left; i <= right; i++) {
                ans.push_back(matrix[top][i]);
            }
            top++;

            // Top to Bottom
            for (int i = top; i <= bottom; i++) {
                ans.push_back(matrix[i][right]);
            }
            right--;

            // Right to Left
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    ans.push_back(matrix[bottom][i]);
                }
                bottom--;
            }

            // Bottom to Top
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    ans.push_back(matrix[i][left]);
                }
                left++;
            }
        }
        return ans;
    }
};
