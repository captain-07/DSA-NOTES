---
created: 2026-07-22
revisions:
  - 2026-07-24
  - 2026-07-29
  - 2026-08-06
  - 2026-08-21
---

# Divide Two Numbers Without Multiplication And Division

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Facebook #Amazon #Microsoft #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bitmanipulation [[Bit Manipulation]]
  - #math [[Math]]

---
## Pattern

Bit Manipulation (Doubling / Binary Lifting)

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

Any quotient can be represented as a sum of powers of 2. Instead of subtracting the divisor one by one, shift the divisor left (doubling it: $b \ll 1, b \ll 2, \dots$) to find the largest multiple that fits in the remaining dividend, subtract it, accumulate the multiplier, and repeat.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Use bitwise shifting (`divisor << i`) to find the largest $2^i \times \text{divisor}$ that can be subtracted from the dividend in each outer step, reducing the search space exponentially.

---
## Approach

### Brute Force
- Continuously subtract the absolute `divisor` from the absolute `dividend` until `dividend < divisor`.
- Time Complexity: $O(\text{dividend})$ (causes TLE for large inputs like $2^{31} / 1$).

### Better
- Use binary search to find the quotient in the range $[0, \text{dividend}]$, using addition to simulate multiplication.
- Time Complexity: $O(\log(\text{dividend}) \times \log(\text{dividend}))$ due to simulation of multiplication via repeated addition.

### Optimal
- Determine the sign of the quotient using XOR (`(dividend < 0) ^ (divisor < 0)`).
- Work with absolute values.
- In a loop, find the largest bit shift `i` such that `(divisor << i) <= dividend`.
- Subtract `(divisor << i)` from `dividend`, and add `(1 << i)` to the `quotient`.
- Clamp the final quotient within the 32-bit signed integer range: $[-2^{31}, 2^{31} - 1]$.

---
## Code (Python)

```python
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        # Constants for 32-bit signed integer limits
        INT_MIN, INT_MAX = -2**31, 2**31 - 1

        # Handle 32-bit integer overflow edge case
        if dividend == INT_MIN and divisor == -1:
            return INT_MAX

        # Determine the sign of the result
        is_negative = (dividend < 0) ^ (divisor < 0)

        # Use absolute values
        a, b = abs(dividend), abs(divisor)
        quotient = 0

        # Exponentially subtract multiples of b
        while a >= b:
            temp_divisor = b
            multiplier = 1
            # Double the divisor until doubling it further exceeds the remainder
            while a >= (temp_divisor << 1):
                temp_divisor <<= 1
                multiplier <<= 1

            # Subtract the scaled divisor and add the multiplier
            a -= temp_divisor
            quotient += multiplier

        return -quotient if is_negative else quotient
```

---
## Dry Run (Smart Example)

Input: `dividend = 22`, `divisor = 3` (Absolute values: `a = 22`, `b = 3`, `quotient = 0`)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `temp_divisor = 12` (3 << 2), `multiplier = 4` (1 << 2) | Find largest shift: `3 << 2 = 12 <= 22` but `3 << 3 = 24 > 22`. |
| 2 | `a = 10` (22 - 12), `quotient = 4` | Subtract `temp_divisor` from `a` and add `multiplier` to `quotient`. |
| 3 | `temp_divisor = 6` (3 << 1), `multiplier = 2` (1 << 1) | Next iteration: `3 << 1 = 6 <= 10` but `3 << 2 = 12 > 10`. |
| 4 | `a = 4` (10 - 6), `quotient = 6` (4 + 2) | Subtract `temp_divisor` from `a` and add `multiplier` to `quotient`. |
| 5 | `temp_divisor = 3` (3 << 0), `multiplier = 1` (1 << 0) | Next iteration: `3 << 0 = 3 <= 4` but `3 << 1 = 6 > 4`. |
| 6 | `a = 1` (4 - 3), `quotient = 7` (6 + 1) | Subtract `temp_divisor` from `a` and add `multiplier` to `quotient`. Loop terminates as `a < b` (1 < 3). |

---
## Edge Cases

- **Overflow:** `dividend = -2147483648` and `divisor = -1` (requires returning `2147483647`).
- **Divisor is 1 or -1:** Directly return the bounded dividend or its negation to save time.
- **Dividend < Divisor:** Returns `0` immediately.
- **Negative inputs:** Handled properly by XOR sign calculation and converting inputs to absolute values.

---
## Mistakes

- **User Mistake:** No specific note provided.
- **Integer Overflow:** Forgetting that absolute value of $-2^{31}$ cannot be stored in a standard 32-bit signed integer (must handle quotient bounds at the end).
- **Infinite Loop:** Shifting a 32-bit integer beyond its boundary in languages like C++/Java without using 64-bit casting or boundary checks.

---
## Complexity

Time: O((log N)^2) → The outer loop runs $O(\log(\text{dividend}))$ times, and the inner doubling loop runs up to $O(\log(\text{dividend}))$ times.
Space: O(1) → Only a few variables are used to track the quotient and multipliers.

---
## Similar Problems

- [Pow(x, n)](https://leetcode.com/problems/powx-n/) - Medium
- [Sqrt(x)](https://leetcode.com/problems/sqrtx/) - Easy
- [Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/) - Medium

---
## Tags and Properties

- #dsa #important #revisit
- #bitmanipulation [[Bit Manipulation]]
- #math [[Math]]
- **Revision Date:** 2026-07-22
- **Problem Link:** [LeetCode - Divide Two Integers](https://leetcode.com/problems/divide-two-integers/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-24)
- [ ] Day 7 Revision (2026-07-29)
- [ ] Day 15 Revision (2026-08-06)
- [ ] Day 30 Revision (2026-08-21)
