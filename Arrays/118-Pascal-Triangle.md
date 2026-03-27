# 118. Pascal's Triangle

## 1. Theoretical Concepts & Intuition
Pascal's Triangle is a triangular array where the first and last elements of each row are 1, and each middle element is the sum of the two elements directly above it.

* **Naive Approach:** Use the formula $vector[j] = triangle[i-1][j] + triangle[i-1][j-1]$.
* **Optimized Row Generation:** To generate a row in $O(N)$ without calculating factorials, use the observation:
    $CurrentElement = PreviousElement \times \frac{(n - col)}{col}$
    Example for $n=5$: $1 \rightarrow (1 \times 5/1) = 5 \rightarrow (5 \times 4/2) = 10 \rightarrow (10 \times 3/3) = 10 \rightarrow \dots$


## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Sum of Previous Row** | $O(N^2)$ | $O(N^2)$ |
| **Mathematical (Optimal Row)** | $O(N^2)$ | $O(1)$ (auxiliary) |

## 3. Summary of all Approaches
* **Approach 1 (Basic Simulation):** Create a vector of vectors. For each row, set the first and last elements to 1. Fill middle values by summing the two elements from the previous row.
* **Approach 2 (Mathematical Optimized):** 1. Create a helper function `generateRow(n)` that computes a single row in $O(n)$ using the multiplication/division trick.
    2. Loop from $1$ to $N$ and push each generated row into the result triangle.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    // Helper to generate a specific row in O(N)
    vector<int> generateRow(int row) {
        long long ans = 1;
        vector<int> rowList;
        rowList.push_back(1); // First element is always 1
        for (int col = 1; col < row; col++) {
            ans = ans * (row - col);
            ans = ans / col;
            rowList.push_back((int)ans);
        }
        return rowList;
    }

    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> triangle;
        for (int i = 1; i <= numRows; i++) {
            triangle.push_back(generateRow(i));
        }
        return triangle;
    }
};
