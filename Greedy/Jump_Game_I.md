---
created: 2026-09-21
revisions:
  - 2026-09-23
  - 2026-09-28
  - 2026-10-06
  - 2026-10-21
---

# Jump Game - I

---

## Metadata & Placement Tags

- **Folder:** Greedy
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy]], #array [[Arrays]], #dynamicprogramming [[Dynamic Programming]]

## Pattern

Greedy Max Reach / Interval Coverage

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Maintain a `max_reachable` index as you iterate through the array. At each index `i`, if `i` exceeds `max_reachable`, you're stuck; otherwise, update `max_reachable = max(max_reachable, i + nums[i])`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Track the furthest index reachable. If current index `i > max_reachable`, return `False`. If `max_reachable >= len(nums) - 1`, return `True`.

---

## Approach

### Brute Force
- Recursively check all reachable jump paths starting from index 0 to the end.
- Time: O(2^N) | Space: O(N)

### Better
- Dynamic Programming (Top-Down with Memoization / Bottom-Up DP table storing boolean reachability per index).
- Time: O(N^2) | Space: O(N)

### Optimal
- **Greedy approach**: Iterate through the array keeping track of the `max_reachable` boundary.
- If current position `i` is within `max_reachable`, update `max_reachable`.
- Stop early if `max_reachable` reaches or exceeds the target last index.

---

## Code (Python)

```python
class Solution:
    def canJump(self, nums: list[int]) -> bool:
        max_reachable = 0
        target_index = len(nums) - 1

        for current_index in range(len(nums)):
            # If current position cannot be reached, return False
            if current_index > max_reachable:
                return False

            # Update the maximum reachable index from current position
            max_reachable = max(max_reachable, current_index + nums[current_index])

            # Optimization: If target is reached, return early
            if max_reachable >= target_index:
                return True

        return True
```

---

## Dry Run (Smart Example)

Input: `nums = [2, 3, 1, 0, 4]`

| Step | Variables | Explanation |
|---|---|---|
| Initial | `max_reachable = 0` | Start at index 0 |
| i = 0 | `nums[0] = 2`, `max_reachable = 2` | `0 <= 0`, reach updated to `0 + 2 = 2` |
| i = 1 | `nums[1] = 3`, `max_reachable = 4` | `1 <= 2`, reach updated to `1 + 3 = 4` |
| i = 2 | `max_reachable = 4 >= target (4)` | Early termination, target is reachable |

---

## Edge Cases

- **Single element (`[0]`):** Immediately return `True` (already at end).
- **Starting with zero (`[0, 2, 3]`):** `max_reachable` stays 0; returns `False` at index 1.
- **Zeros causing roadblock (`[3, 2, 1, 0, 4]`):** `max_reachable` caps at index 3; fails to cross index 3.
- **Large jumps (`[10, 0, 0, 0]`):** Instantly reaches end on first iteration.

---

## Mistakes

- Using O(N^2) DP when a single O(N) pass is sufficient.
- Forgetting to check if `i > max_reachable` before processing index `i`.
- User mistake: No specific note provided.

---

## Complexity

Time: O(N) → Single pass through the array.
Space: O(1) → Uses only a few variables for tracking indices.

---

## Similar Problems

- [Jump Game II](https://leetcode.com/problems/jump-game-ii/) - Medium
- [Jump Game VII](https://leetcode.com/problems/jump-game-vii/) - Medium
- [Gas Station](https://leetcode.com/problems/gas-station/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #greedy #arrays
- Obsidian links: [[Greedy]], [[Arrays]], [[Dynamic Programming]]
- **Revision Date:** 2026-09-21
- **Problem Link:** [Jump Game - LeetCode](https://leetcode.com/problems/jump-game/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-23)
- [ ] Day 7 Revision (2026-09-28)
- [ ] Day 15 Revision (2026-10-06)
- [ ] Day 30 Revision (2026-10-21)
