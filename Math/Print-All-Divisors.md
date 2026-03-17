# Print All Divisors

## Method 1: Brute Force
### Intuition
Every number from 1 to $N$ is a potential divisor.

### Strategy
1. Loop from $i = 1$ to $N$.
2. If $N \% i == 0$, print or store $i$.

---

## Method 2: Square Root Method (Optimal)
### Intuition
Divisors occur in pairs $(i, N/i)$. If $i$ is a divisor, then $N/i$ must also be a divisor. One of them is always $\le \sqrt{N}$.

### Strategy
1. Loop from $i = 1$ up to $\sqrt{N}$.
2. If $N \% i == 0$:
   - Add $i$ to a list.
   - If $(N/i) \neq i$, add $(N/i)$ to the list.
3. Sort the list for ordered output.

## Implementation (C++)
```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <algorithm>

class Divisors {
public:
    // Method 1: O(N)
    void printBrute(int n) {
        for (int i = 1; i <= n; i++) {
            if (n % i == 0) std::cout << i << " ";
        }
    }

    // Method 2: O(sqrt(N))
    void printOptimal(int n) {
        std::vector<int> res;
        for (int i = 1; i * i <= n; i++) {
            if (n % i == 0) {
                res.push_back(i);
                if ((n / i) != i) res.push_back(n / i);
            }
        }
        std::sort(res.begin(), res.end());
        for (int val : res) std::cout << val << " ";
    }
};
