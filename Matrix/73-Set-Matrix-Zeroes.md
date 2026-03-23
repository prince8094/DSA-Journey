# 73. Set Matrix Zeroes

## 1. Theoretical Concepts & Intuition
Given an $m \times n$ matrix, if an element is 0, set its entire row and column to 0.

* **The Trap:** If you set rows/columns to 0 immediately while iterating, you will treat those newly created 0s as original 0s, eventually turning the whole matrix into 0.
* **Brute Force Fix:** Use a special marker (like -1) to identify cells that *should* be zero, then convert them later.
* **Better Logic:** Use two separate arrays to "mark" which rows and which columns need to be zeroed.


## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O((N \times M) \times (N + M))$ | $O(1)$ |
| **Better (Marking Arrays)** | $O(N \times M)$ | $O(N + M)$ |

## 3. Summary of all Approaches
* **Approach 1: Brute Force** Iterate through every cell. If cell is 0, mark all elements in that row and column as -1 (if they aren't already 0). Finally, replace all -1s with 0s.
* **Approach 2: Better (Marking Arrays)**
    1. Create two arrays: `row[N]` and `col[M]` initialized to 0.
    2. Traverse the matrix. If `matrix[i][j] == 0`, set `row[i] = 1` and `col[j] = 1`.
    3. Traverse matrix again. If `row[i] == 1` or `col[j] == 1`, set `matrix[i][j] = 0`.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();

        // --- APPROACH 2: BETTER ---
        vector<int> row(n, 0);
        vector<int> col(m, 0);

        // Step 1: Mark the rows and columns
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (matrix[i][j] == 0) {
                    row[i] = 1;
                    col[j] = 1;
                }
            }
        }

        // Step 2: Set zeroes based on marks
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (row[i] == 1 || col[j] == 1) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
};
