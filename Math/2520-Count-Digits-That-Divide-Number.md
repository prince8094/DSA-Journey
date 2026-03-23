# 2520. Count the Digits That Divide a Number

## 1. Theoretical Concepts & Intuition
The problem asks to count how many digits within a number $num$ can divide $num$ evenly (i.e., $num \pmod{digit} == 0$). 

* **Digit Extraction:** We use the modulo operator ($n \pmod{10}$) to get the last digit and integer division ($n / 10$) to discard it.
* **Divisibility Rule:** A number $val$ divides $num$ if the remainder is zero. Since the problem guarantees the input doesn't contain the digit 0, we don't need to handle division-by-zero errors.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Iterative Extraction** | $O(\log_{10} num)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Approach 1 (Digit-by-Digit):** 1. Create a copy of the original number to iterate.
    2. Extract the last digit using `% 10`.
    3. Check if the original `num` is divisible by this digit.
    4. Repeat until all digits are processed.

## 4. Full C++ Code implementations
```cpp
#include <iostream>

class Solution {
public:
    int countDigits(int num) {
        int n = num;
        int count = 0;
        
        while(n > 0) {
            int rem = n % 10; // Extract digit
            if(num % rem == 0) {
                count++;
            }
            n = n / 10; // Move to next digit
        }
        return count;
    }
};
