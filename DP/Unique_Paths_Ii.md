---
created: 2026-11-25
revisions:
  - 2026-11-27
  - 2026-12-02
  - 2026-12-10
  - 2026-12-25
---

# Unique Paths II

---

## Metadata & Placement Tags

- **Folder:** DP
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #dynamicprogramming [[Dynamic Programming]], #matrix [[Matrix DP]], #grid [[Grid]]

---
## Pattern

2D Grid Dynamic Programming / Space-Optimized DP

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

The number of paths to cell `(r, c)` is the sum of paths from `(r-1, c)` and `(r, c-1)`. If `grid[r][c] == 1` (obstacle), paths to that cell are immediately `0`.

---
## ⚡ Quick Recall (VERY IMPORTANT)

If obstacle, set `dp[c] = 0`; else `dp[c] += dp[c - 1]`.

---
## Approach

### Brute Force
- Recursively branch down and right; return 0 if out of bounds or on obstacle, 1 at destination.
- Time Complexity: $O(2^{m + n})$

### Better
- 2D DP Table of size $m \times n$.
- Transition: `dp[r][c] = dp[r-1][c] + dp[r][c-1]` if no obstacle, else `0`.
- Time Complexity: $O(m \times n)$, Space Complexity: $O(m \times n)$

### Optimal
- 1D DP array of size $n$ representing the current row.
- Transition across rows: if `grid[r][c] == 1`, set `dp[c] = 0`; otherwise, add `dp[c - 1]` to `dp[c]`.
- Time Complexity: $O(m \times n)$, Space Complexity: $O(n)$

---
## Code (Python)

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: list[list[int]]) -> int:
        if not obstacleGrid or obstacleGrid[0][0] == 1:
            return 0

        rows = len(obstacleGrid)
        cols = len(obstacleGrid[0])

        # dp[c] stores the number of paths to the current column c
        dp = [0] * cols
        dp[0] = 1  # Base case: starting point

        for r in range(rows):
            for c in range(cols):
                if obstacleGrid[r][c] == 1:
                    # Obstacle found, path count becomes 0
                    dp[c] = 0
                elif c > 0:
                    # Add paths coming from the left cell
                    dp[c] += dp[c - 1]

        return dp[-1]
```

---
## Dry Run (Smart Example)

Input: `obstacleGrid = [[0, 0], [1, 0]]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Init | `dp = [1, 0]` | Start at (0, 0), valid initial state |
| r=0, c=1 | `obstacleGrid[0][1]=0` | `dp[1] += dp[0]` $\rightarrow$ `dp = [1, 1]` |
| r=1, c=0 | `obstacleGrid[1][0]=1` | Obstacle hit! `dp[0] = 0` $\rightarrow$ `dp = [0, 1]` |
| r=1, c=1 | `obstacleGrid[1][1]=0` | `dp[1] += dp[0]` (0+1) $\rightarrow$ `dp = [0, 1]` |

Result: `dp[-1] = 1`

---
## Edge Cases

- `obstacleGrid[0][0] == 1`: Start is blocked, immediately return 0.
- `obstacleGrid[m-1][n-1] == 1`: Destination is blocked, returns 0.
- Single cell `[[0]]`: Start is destination, returns 1.
- Entire row or column blocked: Path drops to 0 across the rest of the grid.

---
## Mistakes

- User Mistake (LC 61): Confusing or mixing up Problem 61 (Rotate List - Linked List two-pointer problem) with Problem 63 (Unique Paths II - Grid DP). Keep list manipulations separate from 2D pathfinding.
- Forgetting to reset `dp[c] = 0` when encountering an obstacle in 1D DP.
- Missing the check for an obstacle right at `(0, 0)`.

---
## Complexity

Time: $O(m \times n)$ → Every cell in the grid is visited exactly once.
Space: $O(n)$ → Only a single 1D array of width $n$ is maintained.

---
## Similar Problems

- [Unique Paths](https://leetcode.com/problems/unique-paths/) - Medium
- [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/) - Medium
- [Dungeon Game](https://leetcode.com/problems/dungeon-game/) - Hard

---
## Tags and Properties

- #dsa #important #revisit #grid-dp #obstacle-grid
- Concepts: [[Dynamic Programming]], [[Matrix DP]]
- Revision Date: 2026-11-25
- **Problem Link:** [Unique Paths II - LeetCode](https://leetcode.com/problems/unique-paths-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-27)
- [ ] Day 7 Revision (2026-12-02)
- [ ] Day 15 Revision (2026-12-10)
- [ ] Day 30 Revision (2026-12-25)
