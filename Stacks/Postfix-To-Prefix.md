# Postfix to Prefix Conversion

## 1. Theoretical Concepts & Intuition
Converting **Postfix** (`AB+`) to **Prefix** (`+AB`) utilizes the left-to-right evaluation strategy.

* **The Core Logic:** We traverse left-to-right. When an operator is found, we pop the two preceding operands ($t_1$ and $t_2$). To form a prefix string, the operator must be placed at the very front.
* **String Formation:** We combine them as `operator + t2 + t1` (since $t_2$ was pushed earlier and logically comes first).

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Left-to-Right Stack** | $O(N)$ | $O(N)$ |

## 3. Summary of all Approaches
* **Approach (Direct Stack Processing):**
    1. Iterate from $i = 0$ to $N-1$.
    2. If `s[i]` is an operand, `push` it.
    3. If `s[i]` is an operator, `pop` $t_1$ and $t_2$.
    4. Concatenate: `s[i] + t2 + t1`.
    5. `push` the new string back onto the stack.

## 4. Full C++ Code implementations
```cpp
#include <string>
#include <stack>

using std::string;
using std::stack;

class Solution {
public:
    string postToPre(string postfix) {
        stack<string> st;
        int n = postfix.length();
        
        for (int i = 0; i < n; i++) {
            if ((postfix[i] >= 'A' && postfix[i] <= 'Z') || 
                (postfix[i] >= 'a' && postfix[i] <= 'z') || 
                (postfix[i] >= '0' && postfix[i] <= '9')) {
                st.push(string(1, postfix[i]));
            } 
            else {
                // Operator encountered
                string t1 = st.top(); st.pop();
                string t2 = st.top(); st.pop();
                
                // Form prefix: Operator + Operand1 (t2) + Operand2 (t1)
                string con = postfix[i] + t2 + t1;
                st.push(con);
            }
        }
        return st.top();
    }
};
