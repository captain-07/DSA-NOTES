---
created: 2026-11-09
revisions:
  - 2026-11-11
  - 2026-11-16
  - 2026-11-24
  - 2026-12-09
---

# House Robber

---

## Metadata & Placement Tags

- **Folder:** DP
- **Target Companies:** #Amazon #Google #Microsoft #Apple #Meta
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #dynamicprogramming [[Dynamic Programming]], #arrays [[Arrays]]

## Pattern

1D Dynamic Programming / State Reduction

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

At each house `i`, you face a binary decision: rob it and take `nums[i] + max_loot(i-2)`, or skip it and keep `max_loot(i-1)`. Optimal loot at house `i` is strictly `max(rob_current, skip_current)`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Track two variables: `prev2` (loot up to 2 houses back) and `prev1` (loot up to last house). `curr = max(prev1, prev2 + num)`.

---

## Approach

### Brute Force
- Recursively explore all non-adjacent subsets by either choosing or skipping each house.
- Complexity: $O(2^n)$ time, $O(n)$ recursion stack space.

### Better
- Memoize recursive calls (`memo[i]`) or use a 1D DP table of size $n$.
- Complexity: $O(n)$ time, $O(n)$ space.

### Optimal
- Notice each calculation depends only on the previous two values (`prev1` and `prev2`).
- Iterate through each house, compute `curr = max(prev1, prev2 + num)`, update `prev2 = prev1`, `prev1 = curr`.
- Reduces space to $O(1)$.

---

## Code (Python)

```python
class Solution:
    def rob(self, nums: list[int]) -> int:
        if not nums:
            return 0

        # prev2 represents max money robbed up to two houses prior
        # prev1 represents max money robbed up to the previous house
        prev2 = 0
        prev1 = 0

        for current_money in nums:
            # Decide whether to rob current house or skip it
            current_max = max(prev1, prev2 + current_money)
            # Shift window forward
            prev2 = prev1
            prev1 = current_max

        return prev1
```

---

## Dry Run (Smart Example)

Input: `nums = [2, 1, 1, 9]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Initialization | `prev2 = 0`, `prev1 = 0` | Base states before visiting houses. |
| House 0 (`num=2`) | `prev2 = 0`, `prev1 = 2` | `curr = max(0, 0 + 2) = 2`. Rob house 0. |
| House 1 (`num=1`) | `prev2 = 2`, `prev1 = 2` | `curr = max(2, 0 + 1) = 2`. Skip house 1. |
| House 2 (`num=1`) | `prev2 = 2`, `prev1 = 3` | `curr = max(2, 2 + 1) = 3`. Rob house 0 & 2. |
| House 3 (`num=9`) | `prev2 = 3`, `prev1 = 11`| `curr = max(3, 2 + 9) = 11`. Rob house 0 & 3. |

Result: `11`

---

## Edge Cases

- Empty array `[]`: Handled by returning 0 immediately.
- Single element `[5]`: Loop runs once, returns `5`.
- Two elements `[2, 7]`: Returns `max(2, 7) = 7`.
- All elements zero `[0, 0, 0]`: Correctly evaluates to 0 without errors.

---

## Mistakes

- User Mistake: No specific note provided.
- Forgetting that skipping a house allows robbing any previous valid house, not just the strictly alternating ones (e.g., indices `0` and `3`).
- Allocating an unnecessary $O(n)$ array when only the last two states are required.

---

## Complexity

Time: O(n) → Single pass over the array of length $n$.
Space: O(1) → Only two integer variables maintained for states.

---

## Similar Problems

- [House Robber II](https://leetcode.com/problems/house-robber-ii/) - Medium
- [House Robber III](https://leetcode.com/problems/house-robber-iii/) - Medium
- [Delete and Earn](https://leetcode.com/problems/delete-and-earn/) - Medium
- [Maximum Alternating Subsequence Sum](https://leetcode.com/problems/maximum-alternating-subsequence-sum/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #dynamicprogramming #statemachine #linear-dp
- [[Dynamic Programming]] [[State Reduction]]
- **Revision Date:** 2026-11-09
- **Problem Link:** [LeetCode - House Robber](https://leetcode.com/problems/house-robber/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-11)
- [ ] Day 7 Revision (2026-11-16)
- [ ] Day 15 Revision (2026-11-24)
- [ ] Day 30 Revision (2026-12-09)
