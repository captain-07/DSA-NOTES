---
created: 2026-11-02
revisions:
  - 2026-11-04
  - 2026-11-09
  - 2026-11-17
  - 2026-12-02
---

# Frog Jump

---

## Metadata & Placement Tags

- **Folder:** DP
- **Target Companies:**
  - #Google #Amazon #Meta #Microsoft #ByteDance

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #dp [[Dynamic Programming]], #hashmap [[HashMap]], #hashset [[HashSet]]

## Pattern

DP with Hash Set / Reachability Graph DP

---
## Difficulty

Hard
#hard

---

## ⚡ Key Idea (Core Insight)

Maintain a mapping of `stone_position -> set of incoming jump sizes (k)`. For each stone and jump size `k`, the frog can jump to `stone + k - 1`, `stone + k`, and `stone + k + 1` if that target stone exists.

---

## ⚡ Quick Recall (VERY IMPORTANT)

State is `(current_stone, jump_size)`. Track valid `k` per stone in a hash map; jump sizes can only ever be `k - 1, k, k + 1` (with `k > 0`).

---

## Approach

### Brute Force
- Recursively explore all branches: `jump(stone, k) -> jump(next_stone, k-1 / k / k+1)`.
- Time Complexity: $O(3^N)$ where $N$ is the number of stones.

### Better
- Memoize recursive calls with state `(stone_index, k)` using a hash set / cache.
- Improvement Idea: Avoid recomputing overlapping states. Complexity: $O(N^2)$ time and space.

### Optimal
- Iterative DP using a hash map `stone_to_jumps`:
  1. Map each stone position to an empty set of possible jump sizes.
  2. Base case: `stone_to_jumps[0] = {0}`.
  3. Iterate through each stone: for every `k` in its set, check target stones `curr_stone + step` where `step ∈ {k - 1, k, k + 1}` and `step > 0`.
  4. If target exists in map, add `step` to its set.
  5. If last stone's set is non-empty, return `True`.

---

## Code (Python)

```python
class Solution:
    def canCross(self, stones: list[int]) -> bool:
        # Quick validation: second stone must be at position 1 (first jump is always 1)
        if len(stones) > 1 and stones[1] != 1:
            return False

        # Map each stone to the set of jump sizes that can reach it
        stone_to_jumps = {}
        for stone in stones:
            stone_to_jumps[stone] = set()

        # Starting state: on stone 0 with an initial jump of 0
        stone_to_jumps[0].add(0)

        for current_stone in stones:
            for jump in stone_to_jumps[current_stone]:
                # Try all three jump possibilities: k - 1, k, k + 1
                for step in (jump - 1, jump, jump + 1):
                    if step > 0:
                        target_stone = current_stone + step
                        if target_stone in stone_to_jumps:
                            stone_to_jumps[target_stone].add(step)

        # Reached the last stone if it has at least one valid incoming jump
        last_stone = stones[-1]
        return len(stone_to_jumps[last_stone]) > 0
```

---

## Dry Run (Smart Example)

Input: `stones = [0, 1, 3, 5, 6, 8, 12, 17]`

| Step | Current Stone & Jumps | Transitions Evaluated | Map State Updates |
| :--- | :--- | :--- | :--- |
| 1 | `0` with `{0}` | `step = 1` -> target `1` | `1: {1}` |
| 2 | `1` with `{1}` | `step ∈ {1, 2}` -> target `2` (no), target `3` (yes) | `3: {2}` |
| 3 | `3` with `{2}` | `step ∈ {1, 2, 3}` -> target `4` (no), `5` (yes), `6` (yes) | `5: {2}`, `6: {3}` |
| 4 | `5` with `{2}` | `step ∈ {1, 2, 3}` -> target `6` (yes), `7` (no), `8` (yes) | `6: {3, 1}`, `8: {3}` |
| 5 | `6` with `{1, 3}` | From `k=1`: target `7, 8`. From `k=3`: target `8, 9, 10`. | `8: {3, 2}` |

---

## Edge Cases

- `stones[1] != 1`: Frog can only jump 1 unit initially; immediate `False`.
- `len(stones) == 2` with `[0, 1]`: Trivially `True`.
- Large gaps between adjacent stones (`stones[i] - stones[i-1] > i`): Unreachable, sets remain empty.
- `step <= 0`: Must filter out non-positive jump lengths (cannot jump backward or stay in place).

---

## Mistakes

- User Mistake: No specific note provided.
- Forgetting that the first jump must strictly be of size `1`.
- Allowing `step = 0` (causes infinite loops or invalid stationary jumps).
- Using array indexing instead of a hash map (stone values can be up to $2^{31} - 1$).

---

## Complexity

Time: O(N^2) → At most $N$ stones, and stone $i$ can receive at most $i$ unique jump sizes.
Space: O(N^2) → The hash map stores sets containing at most $N$ jump lengths per stone.

---

## Similar Problems

- [Jump Game](https://leetcode.com/problems/jump-game/) - Medium
- [Jump Game II](https://leetcode.com/problems/jump-game-ii/) - Medium
- [Minimum Jumps to Reach Home](https://leetcode.com/problems/minimum-jumps-to-reach-home/) - Medium
- [Maximum Number of Jumps to Reach the Last Index](https://leetcode.com/problems/maximum-number-of-jumps-to-reach-the-last-index/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #dp #hard #hashmap
- [[Dynamic Programming]] [[HashSet]] [[Graph Search]]
- **Revision Date:** 2026-11-02
- **Problem Link:** [LeetCode 403 - Frog Jump](https://leetcode.com/problems/frog-jump/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-04)
- [ ] Day 7 Revision (2026-11-09)
- [ ] Day 15 Revision (2026-11-17)
- [ ] Day 30 Revision (2026-12-02)
