# Greatest Common Divisor (GCD / HCF)

## Method 1: Brute Force
### Intuition
The GCD is the largest number that divides both $n1$ and $n2$. We check every number starting from 1 up to the smaller of the two.

### Strategy
1. Iterate from $i = 1$ to $\min(n1, n2)$.
2. If $n1 \% i == 0$ and $n2 \% i == 0$, update the `gcd` variable.
3. The last value stored is the greatest common divisor.

---

## Method 2: Euclidean Algorithm (Optimal)
### Intuition
Based on the property $GCD(a, b) = GCD(a-b, b)$. The optimized version uses the remainder (modulo) to reach the solution in logarithmic time.

### Strategy
1. While both $a$ and $b$ are $> 0$:
   - If $a > b$, set $a = a \% b$.
   - Else, set $b = b \% a$.
2. When one becomes 0, the other is the $GCD$.

## Implementation (C++)
```cpp
#include <iostream>
#include <algorithm>

class GCD {
public:
    // Method 1: Brute Force - O(min(n1, n2))
    int findGCD_Brute(int n1, int n2) {
        int gcd = 1;
        for (int i = 1; i <= std::min(n1, n2); i++) {
            if (n1 % i == 0 && n2 % i == 0) {
                gcd = i;
            }
        }
        return gcd;
    }

    // Method 2: Euclidean Algorithm - O(log(min(a, b)))
    int findGCD_Optimal(int a, int b) {
        while (a > 0 && b > 0) {
            if (a > b) a = a % b;
            else b = b % a;
        }
        return (a == 0) ? b : a;
    }
};
