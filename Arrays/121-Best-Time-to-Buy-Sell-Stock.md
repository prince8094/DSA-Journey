# 121. Best Time to Buy and Sell Stock

## 1. Theoretical Concepts & Intuition
To maximize profit, you must buy at the lowest possible price seen *so far* and sell at the highest possible price *after* that buy date.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Single Pass** | $O(n)$ | $O(1)$ |

## 3. Summary of all Approaches
* **Greedy Approach:**
    1. Maintain `minPrice` seen so far.
    2. Calculate `profit = currentPrice - minPrice`.
    3. Update `maxProfit` and `minPrice` at each step.

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>

using std::vector;
using std::max;
using std::min;

class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_profit = 0;
        int min_price = prices[0];

        for (int i = 0; i < prices.size(); i++) {
            // Calculate potential profit
            max_profit = max(max_profit, prices[i] - min_price);
            // Update minimum price seen so far
            min_price = min(min_price, prices[i]);
        }
        return max_profit;
    }
};
