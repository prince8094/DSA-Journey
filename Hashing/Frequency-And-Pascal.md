# Hashing & Combinatorics (Pascal's Triangle)

## 1. Theoretical Concepts & Intuition
This set of notes covers two primary areas: Frequency tracking using Hashing/Maps and Combinatorial calculations using Pascal's Triangle.

* **Hashing:** The process of "pre-storing" and "fetching". It allows us to count occurrences (frequency) of elements in $O(1)$ time.
    * **Number Hashing:** Uses an array where the index represents the number.
    * **Character Hashing:** Maps characters to indices. For lowercase 'a'-'z', we use `ch - 'a'` to map to indices $0-25$.
* **Maps vs. Unordered Maps:** * `std::map` stores keys in **sorted order** using a Red-Black Tree.
    * `std::unordered_map` uses a **Hash Table**, providing faster access on average.
* **nCr (Combinations):** Used to find the number of ways to choose $r$ items from $n$. This is the foundation for Pascal's Triangle.
* **Pascal's Triangle:** A triangular array where each number is the sum of the two directly above it. 
    * Any element at row $R$ and column $C$ can be calculated using $(R-1)C(C-1)$.


---

## 2. Time/Space Complexity Table
| Operation / Structure | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Array Hashing** | $O(1)$ (Fetch/Store) | $O(\text{Max\_Element})$ |
| **std::map** | $O(\log N)$ | $O(N)$ |
| **std::unordered\_map** | $O(1)$ (Avg) / $O(N)$ (Worst) | $O(N)$ |
| **nCr Calculation** | $O(r)$ | $O(1)$ |
| **Print Nth Row (nCr App)** | $O(N \times r)$ | $O(1)$ |

---

## 3. Summary of all Approaches
* **Approach 1: Character Hashing (Lowercase only)**
    Create an array of size 26. Subtract 'a' from the character to get the index: `hash[s[i] - 'a']++`.
* **Approach 2: Global vs Local Array Size**
    Inside `main`, integer arrays can be ~ $10^6$ and boolean ~ $10^7$. Globally, they can be larger ($10^7$ and $10^8$ respectively).
* **Approach 3: Map Iteration**
    Use `it.first` for the key and `it.second` for the frequency.
* **Approach 4: Optimized nCr Function**
    Instead of calculating full factorials (which overflow), use the property: $\frac{n \times (n-1) \times \dots}{r \times (r-1) \times \dots}$.

---

## 4. Full C++ Code implementations

```cpp
#include <iostream>
#include <vector>
#include <map>
#include <unordered_map>

using std::cout;
using std::endl;
using std::vector;
using std::map;
using std::unordered_map;
using std::string;

// --- COMBINATORICS: nCr ---
long long nCr(int n, int r) {
    long long res = 1;
    for (int i = 0; i < r; i++) {
        res = res * (n - i);
        res = res / (i + 1);
    }
    return res;
}

// --- PASCAL'S TRIANGLE APPLICATIONS ---
void printNthRow(int n) {
    // Row is 1-indexed in many contexts, adjusted to 0-indexed logic
    for (int c = 1; c <= n; c++) {
        cout << nCr(n - 1, c - 1) << " ";
    }
    cout << endl;
}

int main() {
    // --- CHARACTER HASHING ---
    string s = "abcdabe";
    int hash[26] = {0};
    for (int i = 0; i < s.size(); i++) {
        hash[s[i] - 'a']++;
    }

    // --- MAP FOR FREQUENCY ---
    int arr[] = {1, 2, 3, 1, 2, 1};
    map<int, int> mpp; // Sorted order
    for (int i = 0; i < 6; i++) {
        mpp[arr[i]]++;
    }

    // Iterating in map
    for (auto it : mpp) {
        cout << it.first << " -> " << it.second << endl;
    }

    // --- UNORDERED MAP ---
    unordered_map<int, int> umpp; // Average O(1)
    for (int i = 0; i < 6; i++) {
        umpp[arr[i]]++;
    }

    return 0;
}
