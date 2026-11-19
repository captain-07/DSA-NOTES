---
created: 2026-11-19
revisions:
  - 2026-11-21
  - 2026-11-26
  - 2026-12-04
  - 2026-12-19
---

# Unique Paths

---

## Metadata & Placement Tags

- **Folder:** DP
- **Target Companies:**
  - #Google #Amazon #Microsoft #Meta #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #dp [[Dynamic Programming]], #math [[Combinatorics]], #grid [[Grid Paths]]

## Pattern

Grid Dynamic Programming / Combinatorics

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

To reach cell `(r, c)`, you can only arrive from top `(r - 1, c)` or left `(r, c - 1)`. Total paths to `(r, c)` is the sum of paths to those two adjacent cells, or mathematically, choosing $(m - 1)$ downs out of $(m + n - 2)$ total steps: $\binom{m + n - 2}{m - 1}$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`dp[c] = dp[c] + dp[c - 1]` (space-optimized DP), or directly compute $\binom{m + n - 2}{m - 1}$ in $O(\min(m, n))$ time.

---

## Approach

### Brute Force
- Recursively branch down and right at each step until reaching bottom-right.
- Time Complexity: $O(2^{m + n})$

### Better
- 2D DP table where `dp[r][c] = dp[r-1][c] + dp[r][c-1]`, initialized with 1s along top row and left column.
- Time Complexity: $O(m \times n)$, Space: $O(m \times n)$

### Optimal

#### 1. Space-Optimized Dynamic Programming
- Maintain a single 1D row array of size $n$ initialized to 1s.
- Iterate from row 1 to $m - 1$; update each cell by adding the value from the left: `current_row[col] += current_row[col - 1]`.

#### 2. Combinatorics (Math)
- Total steps required is $(m - 1) + (n - 1) = m + n - 2$.
- The number of unique paths equals $\binom{m + n - 2}{m - 1} = \frac{(m + n - 2)!}{(m - 1)! \cdot (n - 1)!}$.

---

## Code (Python)

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # dp[col] stores the number of unique paths to reach the current cell in that column
        row_paths = [1] * n

        # Update row by row from top to bottom
        for row_idx in range(1, m):
            for col_idx in range(1, n):
                # Paths from top (row_paths[col_idx]) + paths from left (row_paths[col_idx - 1])
                row_paths[col_idx] += row_paths[col_idx - 1]

        return row_paths[-1]

    def uniquePathsMath(self, m: int, n: int) -> int:
        # Compute combinations: C(total_steps, down_steps)
        total_steps = m + n - 2
        down_steps = min(m - 1, n - 1)

        ways = 1
        for step in range(1, down_steps + 1):
            ways = ways * (total_steps - step + 1) // step

        return ways
```

---

## Dry Run (Smart Example)

Input: `m = 3`, `n = 3`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Initial | `row_paths = [1, 1, 1]` | Base row (row 0): only 1 way to reach any cell in the top row. |
| Row 1 | `col = 1`: `1 + 1 = 2`<br>`col = 2`: `1 + 2 = 3` | `row_paths` becomes `[1, 2, 3]`. |
| Row 2 | `col = 1`: `2 + 1 = 3`<br>`col = 2`: `3 + 3 = 6` | `row_paths` becomes `[1, 3, 6]`. |
| Result | Return `row_paths[2] = 6` | Total unique paths from top-left to bottom-right is 6. |

---

## Edge Cases

- `m = 1, n = 1`: Start is destination; result is 1.
- `m = 1, n > 1` or `m > 1, n = 1`: Single line grid; only 1 valid path (all right or all down).
- Large $m, n$ ($m, n \le 100$): Intermediate factorial values can overflow in languages like C++/Java; compute iteratively or use DP.

---

## Mistakes

- User Mistake: No specific note provided.
- Forgetting to 0-index or subtract 1 for total steps: using $m + n$ steps instead of $m + n - 2$.
- Attempting standard recursion without memoization, leading to Time Limit Exceeded (TLE).
- Performing integer division before multiplication in combinatorics, causing truncation errors.

---

## Complexity

Time: O(m * n) for DP / O(min(m, n)) for Math → DP visits each cell once; Math computes combinations in $\min(m - 1, n - 1)$ steps.
Space: O(n) for DP / O(1) for Math → DP requires a single 1D array of size $n$; Math uses constant extra variables.

---

## Similar Problems

- [Unique Paths II](https://leetcode.com/problems/unique-paths-ii/) - Medium
- [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/) - Medium
- [Dungeon Game](https://leetcode.com/problems/dungeon-game/) - Hard
- [Cherry Pickup](https://leetcode.com/problems/cherry-pickup/) - Hard

---

## Tags and Properties

- #dsa #important #revisit #dynamic-programming #combinatorics
- [[Dynamic Programming]]
- [[Combinatorics]]
- **Revision Date:** 2026-11-19
- **Problem Link:** [Unique Paths - LeetCode](https://leetcode.com/problems/unique-paths/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-21)
- [ ] Day 7 Revision (2026-11-26)
- [ ] Day 15 Revision (2026-12-04)
- [ ] Day 30 Revision (2026-12-19)
