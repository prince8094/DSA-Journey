# Power Set (Subsets of a String)

## Intuition
To generate all possible subsets of a string of length $n$, we realize there are $2^n$ total subsets. We can map each number from $0$ to $2^n - 1$ to its binary representation. If the $i^{th}$ bit is set (1), we include the $i^{th}$ character of the string in our subset.


## Strategy
1. The total number of subsets is $2^n$, which can be calculated using the left shift operator: `(1 << n)`.
2. Iterate through every number `num` from $0$ to $(2^n - 1)$.
3. For each `num`, check every bit $i$ from $0$ to $n-1$:
   - Use the formula: `if (num & (1 << i))` to check if the $i^{th}$ bit is set.
   - If set, append `s[i]` to the current subset string.
4. Print or store the resulting subset.

## Implementation (C++)
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <cmath>

void printPowerSet(std::string s) {
    int n = s.length();
    int totalSubsets = (1 << n); // **2^n subsets**

    for (int num = 0; num < totalSubsets; num++) {
        std::string sub = "";
        for (int i = 0; i < n; i++) {
            // **Check if the ith bit of num is set**
            if (num & (1 << i)) {
                sub += s[i];
            }
        }
        std::cout << "\"" << sub << "\"" << std::endl;
    }
}
