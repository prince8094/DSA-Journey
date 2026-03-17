# 125. Valid Palindrome

## Method 1: Filtering & Reverse (Better)
### Intuition
Clean the string first, then compare it with its reversed version.

### Strategy
1. Create a `filtered` string containing only `isalnum` characters in `tolower` form.
2. Reverse `filtered` and check if it matches the original `filtered`.

---

## Method 2: Two-Pointer (Optimal)
### Intuition
Check characters from both ends to save memory. Skip non-alphanumeric on the fly.

### Strategy
1. Set `left = 0` and `right = s.length() - 1`.
2. While `left < right`:
   - If `s[left]` is not alphanumeric, `left++`.
   - Else if `s[right]` is not alphanumeric, `right--`.
   - Else, compare characters in lowercase. If mismatch, return `false`.

## Implementation (C++)
```cpp
#include <string>
#include <cctype>

class Solution {
public:
    // Method 2: Two-Pointer - O(N) Time, O(1) Space
    bool isPalindrome(std::string s) {
        int left = 0, right = s.size() - 1;
        while (left < right) {
            if (!isalnum(s[left])) left++;
            else if (!isalnum(s[right])) right--;
            else {
                if (tolower(s[left]) != tolower(s[right])) return false;
                left++;
                right--;
            }
        }
        return true;
    }
};
