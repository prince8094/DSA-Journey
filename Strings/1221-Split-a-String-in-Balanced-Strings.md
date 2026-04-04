# 1221. Split a String in Balanced Strings

## 1. Theoretical Concepts & Intuition
A **balanced string** is defined as a string containing an equal number of 'L' and 'R' characters. The goal is to split a given balanced string into the maximum possible number of smaller balanced substrings.

* **Greedy Approach:** Since we want the *maximum* number of balanced strings, we should "cut" the string as soon as we find a balanced part. 
* **Balance Variable:** We can use a single integer variable to track the net difference between 'L' and 'R'. 
    * Increment the variable for one character (e.g., 'L').
    * Decrement it for the other (e.g., 'R').
* **Zero Crossing:** Every time the balance variable hits **0**, it indicates that the current substring we are traversing has an equal count of 'L's and 'R's, marking a successful split point.


---

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Greedy Greedy Scan** | $O(N)$ | $O(1)$ |

---

## 3. Summary of all Approaches
* **Approach 1 (Greedy Counter):** 1.  Initialize `balance = 0` and `count = 0`.
    2.  Iterate through the string $s$ character by character.
    3.  If the character is 'L', increment `balance`.
    4.  If the character is 'R', decrement `balance`.
    5.  Check if `balance == 0`. If true, increment the `count` of total balanced strings.
    6.  Return `count`.

---

## 4. Full C++ Code implementations
```cpp
#include <string>

using std::string;

class Solution {
public:
    int balancedStringSplit(string s) {
        int balance = 0;
        int count = 0;

        for (int i = 0; i < s.length(); i++) {
            // Step 1: Update balance
            if (s[i] == 'L') {
                balance++;
            } else {
                balance--;
            }

            // Step 2: If balance is 0, we found a balanced substring
            if (balance == 0) {
                count++;
            }
        }

        return count;
    }
};
