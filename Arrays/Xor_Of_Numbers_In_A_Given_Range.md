---
created: 2026-07-25
revisions:
  - 2026-07-27
  - 2026-08-01
  - 2026-08-09
  - 2026-08-24
---

# Xor Of Numbers In A Given Range

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Directi

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #bitmanipulation [[Bit Manipulation]], #math [[Math]]

## Pattern
Prefix XOR (Range Query to Point Query reduction)

---
## Difficulty
Medium #medium

---
## ⚡ Key Idea (Core Insight)
XOR of range `[L, R]` can be computed as `f(R) ^ f(L - 1)`, where `f(N)` represents the prefix XOR from `1` to `N`. The prefix XOR `f(N)` follows a repeating cycle of length 4: `[N, 1, N + 1, 0]`.

---
## ⚡ Quick Recall (VERY IMPORTANT)
`rangeXOR(L, R) = f(R) ^ f(L - 1)` where `f(N)` is `[N, 1, N + 1, 0]` based on `N % 4`.

---
## Approach

### Brute Force
- Linearly iterate from `L` to `R` while maintaining a running XOR sum.
- Time: O(R - L)
- Space: O(1)

### Optimal
- Reduce range query to prefix queries: `XOR(L, R) = prefixXOR(R) ^ prefixXOR(L - 1)`.
- Use the mathematical pattern of `prefixXOR(N)` to evaluate in O(1) time.
- Time: O(1)
- Space: O(1)

---
## Code (Python)

```python
class Solution:
    def computeXOR(self, n: int) -> int:
        """Computes XOR from 1 to n in O(1) using pattern matching."""
        if n < 0:
            return 0
        rem = n % 4
        if rem == 0:
            return n
        elif rem == 1:
            return 1
        elif rem == 2:
            return n + 1
        return 0

    def findRangeXOR(self, left: int, right: int) -> int:
        """Finds XOR of numbers in the range [left, right]."""
        return self.computeXOR(right) ^ self.computeXOR(left - 1)
```

---
## Dry Run (Smart Example)

Input: `left = 3`, `right = 6`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `left = 3`, `right = 6` | Compute `computeXOR(6) ^ computeXOR(2)`. |
| 2 | `computeXOR(6)` | `6 % 4 = 2` -> returns `6 + 1 = 7` (binary `111`). |
| 3 | `computeXOR(2)` | `2 % 4 = 2` -> returns `2 + 1 = 3` (binary `011`). |
| 4 | `7 ^ 3` | `111 ^ 011 = 100` -> returns `4`. (Check: `3 ^ 4 ^ 5 ^ 6 = 4`). |

---
## Edge Cases
- `left == 0`: Handled correctly since `computeXOR(-1)` returns `0`.
- `left == right`: Returns the number itself as `f(L) ^ f(L - 1) = L`.
- Large values (e.g., `right = 10^9`): Handled instantly in O(1) without integer overflow in Python.

---
## Mistakes
- Attempting to loop through the range, leading to TLE for large bounds.
- Forgetting that the optimal approach is bit tricky because it relies on recognizing a mathematical pattern for prefix XOR.
- Off-by-one errors by computing `f(R) ^ f(L)` instead of `f(R) ^ f(L - 1)`.

---
## Complexity
Time: O(1) → Uses basic arithmetic and conditional checks.
Space: O(1) → No extra data structures are allocated.

---
## Similar Problems
- [XOR Queries of a Subarray](https://leetcode.com/problems/xor-queries-of-a-subarray/) - Medium
- [Single Number II](https://leetcode.com/problems/single-number-ii/) - Medium
- [Number of Wonderful Substrings](https://leetcode.com/problems/number-of-wonderful-substrings/) - Medium

---
## Tags and Properties
  - #dsa #important #revisit
  - #bitmanipulation #math #prefixsum
  - [[Bit Manipulation]] [[Math]] [[Prefix Sum]]
  - **Revision Date:** 2026-07-25
  - **Problem Link:** [GeeksforGeeks - XOR of Numbers in a Given Range](https://www.geeksforgeeks.org/find-xor-of-numbers-from-l-to-r/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-27)
- [ ] Day 7 Revision (2026-08-01)
- [ ] Day 15 Revision (2026-08-09)
- [ ] Day 30 Revision (2026-08-24)
