# Prefix to Postfix Conversion

## 1. Theoretical Concepts & Intuition
Converting **Prefix** (`+AB`) to **Postfix** (`AB+`) requires evaluating the string from **right to left**.

* **The Core Logic:** As we move right-to-left, operands are pushed. When an operator is found, the top of the stack ($t_1$) is the first operand, and the next ($t_2$) is the second.
* **String Formation:** To form a postfix string, the operator must be placed at the very end. We combine them as `t1 + t2 + operator`.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Right-to-Left Stack**| $O(N)$ | $O(N)$ |

## 3. Summary of all Approaches
* **Approach (Reverse Stack Processing):**
    1. Iterate from $i = N-1$ down to $0$.
    2. If `s[i]` is an operand, `push` it.
    3. If `s[i]` is an operator, `pop` $t_1$ and $t_2$.
    4. Concatenate: `t1 + t2 + s[i]`.
    5. `push` the new string back onto the stack.

## 4. Full C++ Code implementations
```cpp
#include <string>
#include <stack>

using std::string;
using std::stack;

class Solution {
public:
    string preToPost(string prefix) {
        stack<string> st;
        int n = prefix.length();
        
        // Iterate Right to Left
        for (int i = n - 1; i >= 0; i--) {
            if ((prefix[i] >= 'A' && prefix[i] <= 'Z') || 
                (prefix[i] >= 'a' && prefix[i] <= 'z') || 
                (prefix[i] >= '0' && prefix[i] <= '9')) {
                st.push(string(1, prefix[i]));
            } 
            else {
                // Operator encountered
                string t1 = st.top(); st.pop();
                string t2 = st.top(); st.pop();
                
                // Form postfix: Operand1 (t1) + Operand2 (t2) + Operator
                string con = t1 + t2 + prefix[i];
                st.push(con);
            }
        }
        return st.top();
    }
};
