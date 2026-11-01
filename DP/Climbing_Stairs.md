---
created: 2026-11-01
revisions:
  - 2026-11-03
  - 2026-11-08
  - 2026-11-16
  - 2026-12-01
---

# Climbing Stairs

---

## Metadata & Placement Tags

- **Folder:** DP
- **Target Companies:** #Amazon #Google #Microsoft #Apple #Meta #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #dynamic-programming [[Dynamic Programming]], #fibonacci [[Fibonacci Sequence]], #memoization [[Memoization]]

## Pattern

1D Dynamic Programming / Fibonacci Sequence

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

To reach step `i`, you must come from either step `i - 1` (1 step jump) or step `i - 2` (2 step jump).
Therefore, the recurrence relation is strictly `ways(i) = ways(i - 1) + ways(i - 2)`, which maps directly to the Fibonacci sequence.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`ways[i] = ways[i-1] + ways[i-2]`. Base cases: `1` way for step 1, `2` ways for step 2.

---

## Approach

### Brute Force
- Recursively branch into `solve(n - 1) + solve(n - 2)`.
- Time: $O(2^n)$, Space: $O(n)$ recursion stack.

### Better
- Memoize overlapping subproblems in an array or hash map (Top-Down DP).
- Time: $O(n)$, Space: $O(n)$.

### Optimal
- **Optimal 1 (Bottom-Up 1D Array):** Allocate a DP array of size `n + 1`, prefill bases, and iterate up to `n`.
- **Optimal 2 (Space-Optimized Iterative):** Track only the last two values (`prev1`, `prev2`) using two pointers/variables.

---

## Code (Python)

```python
class Solution:
    def climbStairs_dp_array(self, n: int) -> int:
        # Optimal 1: 1D DP Array (Linear Space)
        if n <= 2:
            return n

        # dp[i] stores the number of distinct ways to reach step i
        dp = [0] * (n + 1)
        dp[1] = 1
        dp[2] = 2

        for step in range(3, n + 1):
            dp[step] = dp[step - 1] + dp[step - 2]

        return dp[n]

    def climbStairs(self, n: int) -> int:
        # Optimal 2: Space-Optimized Variables (Constant Space)
        if n <= 2:
            return n

        # prev2 represents ways to reach (i - 2), prev1 represents (i - 1)
        prev2 = 1  # step 1
        prev1 = 2  # step 2

        for step in range(3, n + 1):
            current = prev1 + prev2
            prev2 = prev1
            prev1 = current

        return prev1
```

---

## Dry Run (Smart Example)

Input: `n = 5`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Init | `prev2 = 1`, `prev1 = 2` | Covers base states for step 1 and step 2 |
| step = 3 | `current = 1 + 2 = 3` | Shift: `prev2 = 2`, `prev1 = 3` |
| step = 4 | `current = 2 + 3 = 5` | Shift: `prev2 = 3`, `prev1 = 5` |
| step = 5 | `current = 3 + 5 = 8` | Shift: `prev2 = 5`, `prev1 = 8`. Loop terminates |

Result: `8`

---

## Edge Cases

- `n = 1`: Base boundary; return `1` directly without loop.
- `n = 2`: Base boundary; return `2` directly without loop.
- `n = 3`: Smallest case requiring iteration; verifies transition logic.

---

## Mistakes

- Forgetting to mention both optimized approaches: 1D DP array ($O(n)$ space) vs. two rolling variables ($O(1)$ space).
- Confusing 0-based indexing with 1-based step numbers in the DP table.
- Using unmemoized recursion, resulting in Time Limit Exceeded ($O(2^n)$).

---

## Complexity

- **Optimal 1 (1D DP):**
  - Time: $O(n)$ → Single loop computing each step from $3$ to $n$.
  - Space: $O(n)$ → Array of size $n + 1$ to store precomputed states.

- **Optimal 2 (Space-Optimized):**
  - Time: $O(n)$ → Single loop from $3$ to $n$.
  - Space: $O(1)$ → Only two state variables maintained in memory.

---

## Similar Problems

- [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) - Easy
- [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/) - Easy
- [House Robber](https://leetcode.com/problems/house-robber/) - Medium
- [Decode Ways](https://leetcode.com/problems/decode-ways/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #dp #fibonacci
- Concepts: [[Dynamic Programming]], [[State Compression]]
- **Last Revised:** 2026-11-01
- **Problem Link:** [Climbing Stairs - LeetCode](https://leetcode.com/problems/climbing-stairs/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-03)
- [ ] Day 7 Revision (2026-11-08)
- [ ] Day 15 Revision (2026-11-16)
- [ ] Day 30 Revision (2026-12-01)
