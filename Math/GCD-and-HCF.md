
# GCD & HCF (Greatest Common Divisor)

## Intuition
Based on my handwritten notes, the Euclidean Algorithm is the most efficient way to find the GCD. Instead of subtracting, we use the modulo operator to reduce the numbers quickly.

[Image of Euclidean algorithm flow chart]

## Strategy
1. Use the property $GCD(a, b) = GCD(a \pmod b, b)$ where $a > b$.
2. Continue the process until one of the numbers becomes $0$.
3. The non-zero number remaining is the GCD.

## Implementation (C++)
```cpp
#include <iostream>

int getGCD(int a, int b) {
    while (a > 0 && b > 0) {
        if (a > b) {
            a = a % b; // **Reduce the larger number using modulo**
        } else {
            b = b % a;
        }
    }
    // **If a is 0, b is GCD; else a is GCD**
    return (a == 0) ? b : a;
}
