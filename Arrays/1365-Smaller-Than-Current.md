# 1365. How Many Numbers Are Smaller Than the Current Number

## 1. Theoretical Concepts & Intuition
The objective is to determine for every element in an array how many other elements are strictly smaller than it. 

* **Linear Comparison:** The most direct way is a nested search. For each element $nums[i]$, we iterate through the rest of the array. If $nums[j] < nums[i]$, we increment a counter. This is simple but inefficient ($O(n^2)$).
* **The Power of Sorting:** If an array is sorted in ascending order, the index of an element represents exactly how many elements precede it. 
    * *Example:* In the sorted array $[1, 3, 5, 8]$, the value $5$ is at index $2$. This indicates there are $2$ numbers smaller than it ($1$ and $3$).
* **Handling Duplicates:** If the array contains duplicates (e.g., $[1, 2, 2, 3]$), the index of the **first** occurrence is what matters. The first $2$ is at index $1$ (correctly showing $1$ smaller number), but the second $2$ is at index $2$ (which would incorrectly suggest $2$ smaller numbers). We use a Hash Map to "lock in" only the first occurrence's index.



---

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(n^2)$ | $O(1)$ |
| **Sorting + Hash Map** | $O(n \log n)$ | $O(n)$ |

---

## 3. Summary of all Approaches
* **Approach 1: Brute Force** Utilizes a nested loop structure. For every index $i$, an inner loop iterates through all $j$ indices to count instances where $nums[j] < nums[i]$.
* **Approach 2: Optimized Sorting** 1.  Copy the input array to a new vector `sorted`.
    2.  Sort the `sorted` vector using $O(n \log n)$ complexity.
    3.  Traverse the `sorted` vector and store the index of the **first occurrence** of each unique number in an `unordered_map`.
    4.  Iterate through the original `nums` array and use the map to fetch the stored index, which corresponds to the count of smaller numbers.

---

## 4. Full C++ Code implementations
```cpp
#include <vector>
#include <algorithm>
#include <unordered_map>

using std::vector;
using std::sort;
using std::unordered_map;

class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        
        // --- APPROACH 1: BRUTE FORCE ---
        /*
        vector<int> ans;
        for(int i = 0; i < nums.size(); i++) {
            int count = 0;
            for(int j = 0; j < nums.size(); j++) {
                if(i != j && nums[j] < nums[i]) {
                    count++;
                }
            }
            ans.push_back(count);
        }
        return ans;
        */

        // --- APPROACH 2: OPTIMIZED (SORTING) ---
        vector<int> sorted = nums;
        sort(sorted.begin(), sorted.end());
        
        unordered_map<int, int> mp;
        
        // Map each number to its first appearing index in the sorted array
        for(int i = 0; i < sorted.size(); i++) {
            // Only store the index if it's the first time we see the number
            if(mp.find(sorted[i]) == mp.end()) {
                mp[sorted[i]] = i;
            }
        }
        
        vector<int> ans;
        // Build result based on original input order
        for(int num : nums) {
            ans.push_back(mp[num]);
        }
        
        return ans;
    }
};
