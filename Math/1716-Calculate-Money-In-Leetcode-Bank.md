# 1716. Calculate Money in Leetcode Bank

## 1. Theoretical Concepts & Intuition
The problem describes a saving pattern that resets and increases every week. 
* **Weekly Cycle:** Each week has 7 days. On the first Monday, the person saves $1. Each day after that, they save $1 more than the previous day.
* **The Monday Increase:** Every new Monday, the starting amount is $1 more than the *previous* Monday's starting amount.
* **Mathematical Pattern:** This is a combination of Arithmetic Progressions (AP). Each week is an AP of 7 terms, and the starting value of each week also forms an AP.


---

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Iterative Simulation** | $O(n)$ | $O(1)$ |
| **Mathematical (Constant Time)** | $O(1)$ | $O(1)$ |

---

## 3. Summary of all Approaches
* **Approach 1 (Iterative Simulation):**
    1. Initialize `totalMoney = 0` and `mondayStart = 1`.
    2. Use a `while` loop to keep track of the remaining days `n`.
    3. Use a nested `for` loop to iterate through the 7 days of the week.
    4. For each day, add the current day's value to `totalMoney` and increment the daily amount.
    5. After each week, increment `mondayStart` to prepare for the next Monday.
* **Approach 2 (Mathematical - Optimization):** Use the sum of AP formula to calculate the total for full weeks and the remaining days separately.

---

## 4. Full C++ Code implementations
```cpp
#include <iostream>

class Solution {
public:
    int totalMoney(int n) {
        int money = 0;
        int start = 1; // Amount put in on Monday
        
        while (n > 0) {
            int curr = start;
            
            // Loop through the week (max 7 days)
            for (int i = 0; i < 7 && n > 0; i++) {
                money += curr;
                curr++;
                n--;
            }
            
            // Increment the starting amount for the next Monday
            start++;
        }
        
        return money;
    }
};
