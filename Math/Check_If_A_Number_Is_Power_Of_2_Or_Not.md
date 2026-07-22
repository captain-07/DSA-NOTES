---
created: 2026-07-22
revisions:
  - 2026-07-24
  - 2026-07-29
  - 2026-08-06
  - 2026-08-21
---

# Check If A Number Is Power Of 2 Or Not

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Google #Microsoft #Meta #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #bitmanipulation [[Bit Manipulation]], #math [[Mathematics]]

---
## Pattern

Bit Manipulation (Bitwise AND trick)

---
## Difficulty

Easy
#easy

---
## ⚡ Key Idea (Core Insight)

A power of 2 in binary has exactly one set bit (e.g., $8 = 1000_2$).
Subtracting 1 flips all bits up to the set bit (e.g., $7 = 0111_2$).
Thus, `n & (n - 1)` clears the lowest set bit and must equal `0` for any power of 2 (given `n > 0`).

---
## ⚡ Quick Recall (VERY IMPORTANT)

`n > 0 and (n & (n - 1)) == 0` checks if `n` is a power of 2 instantly.

---
## Approach

### Brute Force
- Repeatedly divide `n` by 2 while even. If we reach `1`, it is a power of 2.
- Time Complexity: O(log N)
- Space Complexity: O(1)

### Better
- Count the number of set bits. If set bits count is exactly 1 and `n > 0`, it's a power of 2.
- Time Complexity: O(log N)
- Space Complexity: O(1)

### Optimal 1: Bitwise AND with (n - 1)
- Return `True` if `n > 0` and `(n & (n - 1)) == 0`.

### Optimal 2: Bitwise AND with Two's Complement
- Return `True` if `n > 0` and `(n & -n) == n`.

---
## Code (Python)

```python
class Solution:
    # Optimal 1: Clear the only set bit
    def isPowerOfTwo(self, n: int) -> bool:
        return n > 0 and (n & (n - 1)) == 0

    # Optimal 2: Isolate the lowest set bit
    def isPowerOfTwoAlternative(self, n: int) -> bool:
        return n > 0 and (n & -n) == n
```

---
## Dry Run (Smart Example)

Input: `n = -8`, `n = 12`, `n = 16`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `n = -8` | `n > 0` is `False`. Immediately returns `False`. |
| 2 | `n = 12` | `n = 12 (1100_2)`. `n - 1 = 11 (1011_2)`. `12 & 11 = 8 != 0`. Returns `False`. |
| 3 | `n = 16` | `n = 16 (10000_2)`. `n - 1 = 15 (01111_2)`. `16 & 15 = 0`. Returns `True`. |

---
## Edge Cases

- `n <= 0` (e.g. `0`, `-8`): Negative numbers and zero are not powers of 2. Handled by `n > 0`.
- `n = 1`: $2^0 = 1$. Returns `True` as `1 & 0 == 0`.
- Large integers ($2^{30}$): Handled correctly without overflow in Python.

---
## Mistakes

- **Failing to use bit manipulation:** Using slow iterative loops or recursion instead of O(1) bitwise tricks.
- **Forgetting boundary conditions:** Missing the `n > 0` check, which causes `0` or negative values to return incorrect results.
- **Float precision errors:** Attempting to use `log2(n)` which fails for large integers due to floating-point rounding issues.

---
## Complexity

Time: O(1) → Constant time bitwise operations.
Space: O(1) → No extra memory used.

---
## Similar Problems

- [Power of Three](https://leetcode.com/problems/power-of-three/) - Easy
- [Power of Four](https://leetcode.com/problems/power-of-four/) - Easy
- [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/) - Easy

---
## Tags and Properties

- #dsa #important #revisit
- #bitmanipulation #math [[Bit Manipulation]] [[Mathematics]]
- **Revision Date:** 2026-07-22
- **Problem Link:** [Power of Two - LeetCode](https://leetcode.com/problems/power-of-two/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-24)
- [ ] Day 7 Revision (2026-07-29)
- [ ] Day 15 Revision (2026-08-06)
- [ ] Day 30 Revision (2026-08-21)
