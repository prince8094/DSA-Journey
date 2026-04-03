# 3498. Reverse Degree of a String

## 1. Theoretical Concepts & Intuition
The "Reverse Degree" of a string is a custom metric calculated based on character values in a reversed alphabet and their positions within the string.

* **Reversed Alphabet Mapping:** In a standard alphabet, 'a' is 1 and 'z' is 26. In a reversed alphabet, 'a' becomes 26, 'b' becomes 25, and 'z' becomes 1. 
    * Formula for reversed value: $26 - (s[i] - 'a')$.
* **Positional Weight:** Each character's contribution is scaled by its **1-indexed position** in the string (i.e., the first character has position 1, the second has position 2, etc.).
* **Total Sum:** The final result is the sum of $(ReversedValue \times Position)$ for every character in the string.


---

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Linear Scan** | $O(N)$ | $O(1)$ |

---

## 3. Summary of all Approaches
* **Approach 1 (Single Pass):** 1. Initialize `sum = 0`.
    2. Iterate through the string from index $i = 0$ to $s.size() - 1$.
    3. Calculate the reversed alphabet value: `26 - (s[i] - 'a')`.
    4. Multiply this value by the 1-indexed position, which is $(i + 1)$.
    5. Accumulate the product into `sum` and return the result.

---

## 4. Full C++ Code implementations
```cpp
#include <string>

using std::string;

class Solution {
public:
    int reverseDegree(string s) {
        int sum = 0;

        for (int i = 0; i < s.size(); i++) {
            // Step 1: Calculate position in reversed alphabet ('a'=26, 'b'=25...)
            int value = 26 - (s[i] - 'a');
            
            // Step 2: Multiply by 1-indexed position (i + 1) and accumulate
            sum += value * (i + 1);
        }

        return sum;
    }
};
