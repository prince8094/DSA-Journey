# 189. Rotate Array

## 1. Theoretical Concepts & Intuition
Rotating an array by $k$ steps means moving the last $k$ elements to the front. 
A key observation is that if $k > n$, rotating by $k$ is the same as rotating by $k \pmod n$. 


## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Extra Array (Temp)** | $O(n)$ | $O(n)$ |

## 3. Summary of all Approaches
* **Approach 1: Using Temp Array**
    1. Handle large $k$ using $k = k \pmod n$.
    2. Create a temporary copy of the array.
    3. Shift elements into their new positions: the element at index $i$ moves to $(i+k) \pmod n$.
    4. Copy the temp array back to the original.

## 4. Full C++ Code implementations
```cpp
#include <vector>

using std::vector;

class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k = k % n; // **Handle cases where k > n**
        
        vector<int> temp = nums;
        for (int i = 0; i < n; i++) {
            // Formula to find the new position after rotation
            nums[(i + k) % n] = temp[i]; 
        }
    }
};


