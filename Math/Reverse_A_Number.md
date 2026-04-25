---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Reverse A Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Bloomberg #Apple #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #math [[Mathematics]]
  - #digitmanipulation [[Digit Manipulation]]

## Pattern

Digit Extraction (Modulo + Integer Division)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Extract the last digit of the number using `pop = x % 10` and append it to the reversed result using `rev = rev * 10 + pop`. Use integer division `x // 10` to strip the last digit in each iteration.

---

## ⚡ Quick Recall (VERY IMPORTANT)

While `x != 0`: `rev = (rev * 10) + (x % 10)`. Handle negative signs and 32-bit overflow constraints manually.

---

## Approach

### Brute Force
- Convert the integer to a string, reverse the string, and convert back to an integer.
- **Time Complexity:** O(log₁₀N) for conversion and reversal.
- **Space Complexity:** O(log₁₀N) to store the string.

### Optimal
- Use a mathematical loop.
- 1. Store the sign and work with the absolute value (or handle negative modulo carefully).
- 2. Repeatedly extract the last digit: `digit = x % 10`.
- 3. Build result: `res = res * 10 + digit`.
- 4. Update x: `x //= 10`.
- 5. Check for 32-bit integer overflow (`-2^31` to `2^31 - 1`).

---

## Code (Python)

```python
class Solution:
    def reverse(self, x: int) -> int:
        # Define 32-bit integer limits
        MIN_INT, MAX_INT = -2**31, 2**31 - 1
        
        res = 0
        # Use absolute value for easier digit extraction
        temp_x = abs(x)
        
        while temp_x != 0:
            digit = temp_x % 10
            # Check for overflow before updating res
            if res > (MAX_INT - digit) // 10:
                return 0
            
            res = res * 10 + digit
            temp_x //= 10
            
        # Restore sign
        return res if x >= 0 else -res
```

---

## Dry Run (Smart Example)

Input: `x = -123`

| Step | `temp_x` | `digit` | `res` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| Start | 123 | - | 0 | Initialize with absolute value |
| 1 | 12 | 3 | 3 | `0 * 10 + 3 = 3`; x becomes 12 |
| 2 | 1 | 2 | 32 | `3 * 10 + 2 = 32`; x becomes 1 |
| 3 | 0 | 1 | 321 | `32 * 10 + 1 = 321`; loop terminates |
| End | - | - | -321 | Apply original negative sign |

---

## Edge Cases

- **0:** Should return 0 immediately.
- **Negative Numbers:** Ensure the sign is preserved (e.g., -123 -> -321).
- **Trailing Zeros:** 120 should become 21 (0 becomes leading, then disappears).
- **Overflow:** If reversed result exceeds `[−2^31, 2^31 − 1]`, return 0.

---

## Mistakes

- **Overflow Ignored:** Forgetting that the reversed number might exceed 32-bit limits even if the input doesn't.
- **Language Modulo:** Python's `%` operator on negative numbers behaves differently than C++/Java; it's safer to use `abs()`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log₁₀N) → The number of digits in N determines the iterations.  
Space: O(1) → Only a few variables used regardless of input size.

---

## Similar Problems

- [Reverse Integer](https://leetcode.com/problems/reverse-integer/) - Easy
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/) - Easy
- [Reverse Bits](https://leetcode.com/problems/reverse-bits/) - Easy

---

## Tags and Properties
- #dsa #important #revisit  
- #math [[Mathematics]] #digits [[Digits]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Reverse Integer](https://leetcode.com/problems/reverse-integer/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
