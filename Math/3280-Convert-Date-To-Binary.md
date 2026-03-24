# 3280. Convert Date to Binary

## 1. Theoretical Concepts & Intuition
The problem requires converting a Gregorian date in `yyyy-mm-dd` format into a binary string where each part (year, month, and day) is replaced by its binary representation (without leading zeros), separated by hyphens.

* **String Parsing:** We need to extract the numerical values for year, month, and day from specific indices in the input string.
* **Decimal to Binary Conversion:** A number $x$ is converted to binary by repeatedly taking $x \pmod 2$ to find the remainder (bit) and then updating $x = \lfloor x / 2 \rfloor$. Since this generates bits from least significant to most significant, the resulting string must be reversed.
* **Concatenation:** The final result is a combination of these binary strings joined by the '-' character.


---

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Parsing + Iterative Conversion** | $O(1)$ | $O(1)$ |

*Note: Since the input date string length is constant (10 characters) and the maximum year is limited, the operations take constant time.*

---

## 3. Summary of all Approaches
* **Approach 1 (Manual Parsing & Conversion):** 1.  Use `substr()` to isolate "yyyy", "mm", and "dd".
    2.  Convert these substrings to integers using `stoi()`.
    3.  Define a helper function `binary(int x)` that performs the "divide-by-2" algorithm to build a binary string.
    4.  Reverse the binary string to get the correct order.
    5.  Append the three binary results together with hyphens.

---

## 4. Full C++ Code implementations
```cpp
#include <iostream>
#include <string>
#include <algorithm>

using std::string;
using std::to_string;
using std::reverse;
using std::stoi;

class Solution {
public:
    // Helper function to convert integer to binary string
    string binary(int x) {
        string ans = "";
        while(x > 0) {
            int rem = x % 2;
            ans += to_string(rem);
            x = x / 2;
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }

    string convertDateToBinary(string date) {
        // Step 1: Extract year, month, and day using substrings
        int year = stoi(date.substr(0, 4));
        int mon  = stoi(date.substr(5, 2));
        int d    = stoi(date.substr(8, 2));

        // Step 2: Convert each to binary and concatenate
        string ans = "";
        ans += binary(year);
        ans += "-";
        ans += binary(mon);
        ans += "-";
        ans += binary(d);

        return ans;
    }
};
