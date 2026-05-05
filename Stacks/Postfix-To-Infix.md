# Postfix to Infix Conversion

## 1. Theoretical Concepts & Intuition
In a **Postfix** expression, the operator comes *after* its operands (e.g., `AB+`). To convert this to an **Infix** expression (e.g., `(A+B)`), we evaluate the string from **left to right** using a Stack.

* **Operands:** Whenever we encounter an operand (A-Z, a-z, 0-9), we push it onto the stack as a string.
* **Operators:** Whenever we encounter an operator, it must apply to the two most recently seen operands. We pop two elements from the stack. 
    * *Crucial Ordering:* Because of the LIFO property of stacks, the first element popped ($t_1$) is the **second** operand, and the second element popped ($t_2$) is the **first** operand.
    * We combine them in the format: `(t2 + operator + t1)` and push the resulting string back onto the stack.

## 2. Time/Space Complexity Table
| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Stack-based Traversal** | $O(N)$ | $O(N)$ |

*Note: While the loop runs in $O(N)$, string concatenation in C++ takes time proportional to the length of the strings. In the worst case, this adds an $O(N)$ overhead, but the overall time complexity is still bounded by $O(N)$ asymptotically.*

## 3. Summary of all Approaches
* **Approach (Left-to-Right Stack):**
    1. Initialize an empty stack of strings.
    2. Iterate through the postfix string from $i = 0$ to $N-1$.
    3. If `s[i]` is an operand, convert it to a string and `push` it.
    4. If `s[i]` is an operator, `pop` the top two elements ($t_1$ and $t_2$).
    5. Form a new string: `'(' + t2 + s[i] + t1 + ')'`.
    6. `push` this new string back onto the stack.
    7. Return the final string remaining at `stack.top()`.

## 4. Full C++ Code implementations
```cpp
#include <string>
#include <stack>

using std::string;
using std::stack;

class Solution {
public:
    string postToInfix(string postfix) {
        stack<string> st;
        int n = postfix.length();
        
        for (int i = 0; i < n; i++) {
            // Check if character is an operand
            if ((postfix[i] >= 'A' && postfix[i] <= 'Z') || 
                (postfix[i] >= 'a' && postfix[i] <= 'z') || 
                (postfix[i] >= '0' && postfix[i] <= '9')) {
                st.push(string(1, postfix[i]));
            } 
            else {
                // Operator encountered
                string t1 = st.top(); st.pop();
                string t2 = st.top(); st.pop();
                
                // Form infix and push back
                string con = "(" + t2 + postfix[i] + t1 + ")";
                st.push(con);
            }
        }
        return st.top();
    }
};
