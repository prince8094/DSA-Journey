# 9. Palindrome Number

## Intuition
A palindrome reads the same forwards and backwards. In my notebook, I noted that **negative numbers can never be palindromes** due to the minus sign. The strategy is to reverse the integer and compare it with the original.

## Strategy
1. If $x < 0$, return `false`.
2. Use a `long long` for the reversed number to avoid overflow.
3. Extract digits using modulo $10$ and reconstruct the number in reverse.
4. Compare the reversed result with the original input.

## Implementation (C++)
```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) return false; // **Negative numbers are not palindromes**

        long long org = x; 
        long long rev = 0;

        while (x > 0) {
            int lastDigit = x % 10;
            rev = (rev * 10) + lastDigit; // **Critical: Shift existing digits left**
            x /= 10; // **Critical: Integer division to move to next digit**
        }

        return rev == org;
    }
};
