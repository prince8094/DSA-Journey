# Prefix to Infix Conversion

## 1. Theoretical Concepts & Intuition
In a **Prefix** expression, the operator comes *before* its operands (e.g., `+AB`). To convert this to **Infix**, we process the string from **right to left**.

* **Right-to-Left Evaluation:** By reading backwards, we encounter the operands before the operators that apply to them, allowing us to use the exact same stack logic as postfix conversion.
* **Operand Ordering:** Because we are reading right-to-left, the top of the stack ($t_1$) will actually be the **first** operand, and the second element ($t_2$) will be the **second** operand. 
    * We combine them in the format: `(t1 + operator + t2)`.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Reverse Stack Traversal** | $O(N)$ | $O(N)$ |

## 3. Summary of all Approaches
* **Approach (Right-to-Left Stack):**
    1. Iterate from $i = N-1$ down to $0$.
    2. If `s[i]` is an operand, `push` it onto the stack.
    3. If `s[i]` is an operator, `pop` the top two elements ($t_1$ and $t_2$).
    4. Form the infix string: `'(' + t1 + s[i] + t2 + ')'`.
    5. `push` the resulting string back onto the stack.

## 4. Full C++ Code implementations
```cpp
#include <string>
#include <stack>

using std::string;
using std::stack;

class Solution {
public:
    string preToInfix(string prefix) {
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
                
                // Form infix (Note: t1 comes before t2 here)
                string con = "(" + t1 + prefix[i] + t2 + ")";
                st.push(con);
            }
        }
        return st.top();
    }
};
