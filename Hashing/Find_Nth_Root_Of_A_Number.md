---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Find Nth Root Of A Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #DEShaw #Flipkart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #mathematics [[Mathematics]]

## Pattern

Binary Search on Answer (Monotonic Function)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The function $f(x) = x^n$ is **monotonically increasing** for $x \geq 1$. Since the answer must lie between $1$ and $m$, we can treat the range $[1, m]$ as a sorted search space and apply Binary Search to find the value $x$ such that $x^n = m$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Perform Binary Search on range $[1, m]$. For each `mid`, calculate $mid^n$. If it equals $m$, return `mid`; if greater, search left; if smaller, search right.

---

## Approach

### Brute Force
- Iterate $i$ from $1$ to $m$ and check if $i^n == m$. If $i^n > m$, stop and return $-1$.
- **Time Complexity:** $O(m \cdot \log n)$

### Optimal
- Use **Binary Search** on the answer range $[1, m]$.
- Use a helper function `multiply(mid, n, m)` to calculate $mid^n$ while preventing overflow (return 1 if equal, 2 if greater, 0 if smaller).
- Adjust `low` and `high` pointers based on the helper's output.
- **Time Complexity:** $O(\log m \cdot \log n)$

---

## Code (Python)

```python
def getNthRoot(n: int, m: int) -> int:
    # Helper to check mid^n vs m to avoid large number overflow
    def check(mid, n, m):
        ans = 1
        for i in range(1, n + 1):
            ans = ans * mid
            if ans > m: return 2 # Greater than m
        if ans == m: return 1   # Equal to m
        return 0                # Smaller than m

    low = 1
    high = m
    
    while low <= high:
        mid = (low + high) // 2
        mid_pow = check(mid, n, m)
        
        if mid_pow == 1:
            return mid
        elif mid_pow == 0:
            low = mid + 1
        else:
            high = mid - 1
            
    return -1
```

---

## Dry Run (Smart Example)

**Input:** `n = 3, m = 27`

| Step | Low | High | Mid | `mid^n` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 27 | 14 | $2744$ | $14^3 > 27$, set `high = 13` |
| 2 | 1 | 13 | 7 | $343$ | $7^3 > 27$, set `high = 6` |
| 3 | 1 | 6 | 3 | $27$ | $3^3 == 27$, **Return 3** |

---

## Edge Cases

- **$m = 1$:** Always returns $1$ as $1^n = 1$.
- **$n = 1$:** Always returns $m$ as $m^1 = m$.
- **No integer root ($m=5, n=2$):** Should return $-1$.
- **Large $m$ and $n$:** Handled by the `check` function to prevent overflow.

---

## Mistakes

- Using `mid**n` directly in languages like C++/Java which causes integer overflow (use a loop or `pow` with checks).
- Not returning `-1` if the perfect root doesn't exist.
- Incorrectly setting `high` to `m/n` (not applicable for roots).

---

## Complexity

- **Time:** $O(\log m \cdot \log n)$ → $\log m$ for binary search and $\log n$ for the power calculation.
- **Space:** $O(1)$ → No extra space used besides variables.

---

## Similar Problems

- [Sqrt(x)](https://leetcode.com/problems/sqrtx/) - Easy
- [Pow(x, n)](https://leetcode.com/problems/powx-n/) - Medium
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Mathematics]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [GFG: Find Nth Root of M](https://www.geeksforgeeks.org/problems/nth-root-of-m5843/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
