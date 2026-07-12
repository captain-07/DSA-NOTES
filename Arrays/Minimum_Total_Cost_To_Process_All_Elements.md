---
created: 2026-07-12
revisions:
  - 2026-07-14
  - 2026-07-19
  - 2026-07-27
  - 2026-08-11
---

# Minimum Total Cost To Process All Elements

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #math [[Mathematics]], #greedy [[Greedy]]

## Pattern

Arithmetic Progression Sum + Parity Division

---
## Difficulty

Easy
#easy

---
## ⚡ Key Idea (Core Insight)

The total cost to process $n$ elements sequentially is the sum of the first $n$ integers: $1 + 2 + \dots + n = \frac{n(n + 1)}{2}$. To prevent arithmetic overflow when calculating $n(n + 1)$ for large $n$, divide the even factor by 2 before performing the multiplication.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Use $\frac{n(n+1)}{2}$ computed safely: `(n // 2) * (n + 1)` if even, else `n * ((n + 1) // 2)`.

---
## Approach

### Brute Force
Iterate from 1 to $n$ and accumulate the sum.
- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$

### Optimal
Use the arithmetic progression formula with parity check to avoid overflow:
- If $n$ is even, compute `(n // 2) * (n + 1)`.
- If $n$ is odd, compute `n * ((n + 1) // 2)`.
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$

---
## Code (Python)

```python
class Solution:
    def minTotalCost(self, n: int) -> int:
        # Prevent intermediate overflow by dividing the even term first
        if n % 2 == 0:
            return (n // 2) * (n + 1)
        else:
            return n * ((n + 1) // 2)
```

---
## Dry Run (Smart Example)

Input: `n = 5`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `n = 5` | Odd input. Selects the formula `n * ((n + 1) // 2)`. |
| 2 | `n + 1 = 6` | Computes the even factor. |
| 3 | `6 // 2 = 3` | Divides the even factor first to avoid large multiplication. |
| 4 | `5 * 3 = 15` | Multiplies 5 by 3 to get final result 15. |

---
## Edge Cases

- `n = 0`: Returns 0 (no elements to process).
- `n = 1`: Returns 1 (single element).
- `n = 2 * 10^9`: Safe calculation avoids 64-bit integer overflow on intermediate multiplication.

---
## Mistakes

- Not identifying the AP sum formula $1 + 2 + \dots + n = \frac{n(n+1)}{2}$.
- Multiplying $n * (n + 1)$ first, which can cause overflow for large $n$ before the division by 2 occurs.
- Forgetting to handle even and odd cases separately for early division (`n // 2` or `(n + 1) // 2`).

---
## Complexity

Time: O(1) → Constant time mathematical evaluation.
Space: O(1) → Constant auxiliary space.

---
## Similar Problems

- [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/) - Easy
- [Sum of All Odd Length Subarrays](https://leetcode.com/problems/sum-of-all-odd-length-subarrays/) - Easy
- [Calculate Money in Leetcode Bank](https://leetcode.com/problems/calculate-money-in-leetcode-bank/) - Easy

---
## Tags and Properties
- #dsa #important #revisit #math #greedy
- [[Mathematics]] [[Greedy]]
- **Revision Date:** 2026-07-12
- **Problem Link:** [Sum of First N Natural Numbers](https://practice.geeksforgeeks.org/problems/sum-of-series9556/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-14)
- [ ] Day 7 Revision (2026-07-19)
- [ ] Day 15 Revision (2026-07-27)
- [ ] Day 30 Revision (2026-08-11)
