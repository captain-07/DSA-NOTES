---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Find Nth Root Of A Number

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Samsung #Adobe
- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #math [[Mathematics]]

## Pattern

Binary Search on Answer

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The function $f(x) = x^n$ is **monotonically increasing** for $x \ge 1$. Since we need to find an integer $x$ such that $x^n = m$, we can perform a binary search over the range $[1, m]$ to find the value that satisfies the equation.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Perform **Binary Search** in range $[1, m]$. Use a helper function for $mid^n$ to **avoid overflow** by returning "greater than $m$" immediately if the product exceeds the target.

---

## Approach

### Brute Force
- Linearly check every number $i$ from $1$ to $m$ if $pow(i, n) == m$.
- Time Complexity: $O(m \cdot n)$

### Optimal
- Use Binary Search on the range $[1, m]$.
- For each `mid`, calculate $mid^n$ carefully.
- If $mid^n == m$, return `mid`. If $mid^n < m$, search right; else search left.
- Time Complexity: $O(n \cdot \log m)$

---

## Code (Python)

```python
class Solution:
    def nthRoot(self, n: int, m: int) -> int:
        # Helper to check mid^n vs m without overflow
        # Returns: 0 if < m, 1 if == m, 2 if > m
        def compare(mid, n, m):
            ans = 1
            for _ in range(n):
                ans *= mid
                if ans > m:
                    return 2
            return 1 if ans == m else 0

        low, high = 1, m
        while low <= high:
            mid = (low + high) // 2
            res = compare(mid, n, m)
            
            if res == 1:
                return mid
            elif res == 0:
                low = mid + 1
            else:
                high = mid - 1
                
        return -1
```

---

## Dry Run (Smart Example)

**Input:** $n = 3, m = 27$

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `low=1, high=27, mid=14` | $14^3 = 2744$. Since $2744 > 27$, set `high = 13`. |
| 2 | `low=1, high=13, mid=7` | $7^3 = 343$. Since $343 > 27$, set `high = 6`. |
| 3 | `low=1, high=6, mid=3` | $3^3 = 27$. Since $27 == 27$, **Return 3**. |

---

## Edge Cases

- **$m = 1$:** Always returns $1$ as $1^n = 1$.
- **$n = 1$:** Always returns $m$ as $m^1 = m$.
- **No Integer Root:** $n=2, m=5 \implies$ Returns $-1$.
- **Large $m$:** Binary search handles large ranges efficiently ($O(\log m)$).

---

## Mistakes

- **Overflow:** Calculating `pow(mid, n)` directly can crash or overflow before comparison. Use a loop with early exit.
- **Range:** Don't forget the search space is $[1, m]$, not $[1, n]$.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(n \cdot \log m)$ → Binary search takes $\log m$ steps, each requiring $n$ multiplications.  
Space: $O(1)$ → Constant space for variables.

---

## Similar Problems

- [Sqrt(x)](https://leetcode.com/problems/sqrtx/) - Easy
- [Pow(x, n)](https://leetcode.com/problems/powx-n/) - Medium
- [Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch [[Binary Search]] #math [[Mathematics]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Nth Root of a Number - GFG](https://www.geeksforgeeks.org/problems/nth-root-of-a-number3235/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
