---
created: 2026-11-27
revisions:
  - 2026-11-29
  - 2026-12-04
  - 2026-12-12
  - 2026-12-27
---

# Subset Sum Equals To Target

---

## Metadata & Placement Tags

- **Folder:** DP
- **Target Companies:**
  - #Amazon #Microsoft #Google #Adobe #Flipkart

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #dynamic-programming [[Dynamic Programming]], #knapsack [[0-1 Knapsack]], #recursion [[Recursion]]

## Pattern

0/1 Knapsack (Pick / Non-Pick) + 1D Space Optimization

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

At each element, choose to either **include** it (`dp[target - num]`) or **exclude** it (`dp[target]`). A boolean state `dp[s]` tracks whether a subset sum of `s` is achievable using a prefix of the array.

---

## ⚡ Quick Recall (VERY IMPORTANT)

0/1 Knapsack style: iterate numbers forward, iterate target backwards from `target` down to `num` to reuse previous row states in 1D array.

---

## Approach

### Brute Force
- Recursively explore both choices (pick / not pick) for each element.
- Time Complexity: $O(2^N)$

### Better
- Memoized top-down recursion storing results in a 2D table `memo[index][current_sum]`.
- Time: $O(N \times \text{target})$, Space: $O(N \times \text{target}) + O(N)$ recursion stack.

### Optimal
- Space-optimized bottom-up DP using a 1D boolean array of size `target + 1`.
- Base state: `dp[0] = True`.
- For each `num`, update `dp[s] = dp[s] or dp[s - num]` in reverse direction (`target` down to `num`).

---

## Code (Python)

```python
class Solution:
    def isSubsetSum(self, nums: list[int], target: int) -> bool:
        # dp[s] represents whether a subset sum equal to 's' is possible
        dp = [False] * (target + 1)

        # Base case: sum of 0 is always possible with an empty subset
        dp[0] = True

        for num in nums:
            # Iterate backwards to ensure each number is used at most once
            for current_sum in range(target, num - 1, -1):
                if dp[current_sum - num]:
                    dp[current_sum] = True

        return dp[target]
```

---

## Dry Run (Smart Example)

Input: `nums = [3, 34, 4, 12, 5, 2]`, `target = 9`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `num = 3` | Updates `dp[3] = True` because `dp[0]` is True. |
| 2 | `num = 4` | Updates `dp[7] = True` (via `dp[3]`), `dp[4] = True` (via `dp[0]`). |
| 3 | `num = 5` | Updates `dp[9] = True` (via `dp[4]`), `dp[8] = True` (via `dp[3]`). Target 9 reached. |
| 4 | Final Check | `dp[9]` is True; algorithm returns `True`. |

---

## Edge Cases

- `target == 0`: Always return `True` (empty subset).
- `any(num > target)`: Safely ignored when iterating down to `num`.
- `sum(nums) < target`: Impossible to form target; can return `False` early.
- Single element equal to target: Directly sets `dp[target] = True`.

---

## Mistakes

- User Mistake: No specific note provided.
- Iterating `current_sum` forwards instead of backwards in 1D array (turns it into Unbounded Knapsack).
- Forgetting that `dp[0] = True` as the initial reachable state.

---

## Complexity

Time: O(N × target) → Nested loops over N elements and target sums.
Space: O(target) → 1D DP table of size target + 1.

---

## Similar Problems

- [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) - Medium
- [Target Sum](https://leetcode.com/problems/target-sum/) - Medium
- [Coin Change II](https://leetcode.com/problems/coin-change-ii/) - Medium
- [Last Stone Weight II](https://leetcode.com/problems/last-stone-weight-ii/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #dp #knapsack #subset-sum
- [[Dynamic Programming]] [[Knapsack]] [[Subset Sum]]
- **Last Revised:** 2026-11-27
- **Problem Link:** [GeeksforGeeks - Subset Sum Problem](https://www.geeksforgeeks.org/problems/subset-sum-problem-1611555638/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-29)
- [ ] Day 7 Revision (2026-12-04)
- [ ] Day 15 Revision (2026-12-12)
- [ ] Day 30 Revision (2026-12-27)
