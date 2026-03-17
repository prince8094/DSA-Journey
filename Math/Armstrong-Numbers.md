# Armstrong Numbers

## Intuition
An Armstrong number (like 153 or 1634) is a number that equals the sum of its own digits each raised to the power of the number of digits. 

## Strategy
1. Count the total number of digits ($k$).
2. Extract each digit using modulo 10.
3. Raise the digit to the power of $k$ and add to a running `sum`.
4. Check if `sum == original_number`.
5. Complexity AnalysisTime Complexity: O(\log_{10} N) Space Complexity: O(1)

## Implementation (C++)
```cpp
#include <iostream>
#include <cmath>
#include <string>

bool isArmstrong(int n) {
    int duplicate = n;
    int sum = 0;
    // **Count digits to determine the power**
    int k = std::to_string(n).length(); 

    while (n > 0) {
        int lastDigit = n % 10;
        sum += std::pow(lastDigit, k); // **Add power of digit**
        n /= 10;
    }
    return (sum == duplicate);
}
