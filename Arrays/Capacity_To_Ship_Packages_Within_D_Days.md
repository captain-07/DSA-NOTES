---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Capacity To Ship Packages Within D Days

---

## Pattern

Binary Search on Answer (Monotonic Range) + Greedy Verification

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The required capacity has a **monotonic property**: if a capacity `X` works, any capacity `> X` also works. If `X` doesn't work, any capacity `< X` won't either. This allows us to binary search for the minimum valid capacity within the range `[max(weights), sum(weights)]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary search on the **result range** (min capacity to max possible) and use a greedy `canShip(mid)` helper to count required days.

---

## Approach

### Brute Force
- Start from `max(weights)` and check every integer capacity until one works for `D` days.
- **Time Complexity:** $O(\text{range} \times N)$ where range is `sum(weights) - max(weights)`.

### Optimal
- Use **Binary Search on Answer**.
- **Range:** `low = max(weights)` (must carry the heaviest item) to `high = sum(weights)` (ship everything in one day).
- For each `mid` (candidate capacity), greedily pack items into days. If days used $\le D$, the capacity is feasible; try smaller. Otherwise, increase capacity.
- **Time Complexity:** $O(N \log(\sum \text{weights}))$.

---

## Code (Python)

```python
class Solution:
    def shipWithinDays(self, weights: list[int], days: int) -> int:
        # Minimum capacity must be at least the heaviest package
        # Maximum capacity is shipping everything in 1 day
        low, high = max(weights), sum(weights)
        ans = high
        
        def canShip(capacity: int) -> bool:
            days_needed = 1
            current_load = 0
            for w in weights:
                if current_load + w > capacity:
                    days_needed += 1
                    current_load = w
                else:
                    current_load += w
            return days_needed <= days

        while low <= high:
            mid = (low + high) // 2
            if canShip(mid):
                ans = mid # Try to find a smaller feasible capacity
                high = mid - 1
            else:
                low = mid + 1 # Need more capacity
        
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `weights = [3,2,2,4,1,4], days = 3`  
**Initial Range:** `low = 4, high = 16`

| Step | Mid (Cap) | Calculation (Days Needed) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 10 | `[3,2,2], [4,1,4]` (2 days) | $2 \le 3$, Feasible. `high = 9`, `ans = 10` |
| 2 | 6 | `[3,2], [2,4], [1,4]` (3 days) | $3 \le 3$, Feasible. `high = 5`, `ans = 6` |
| 3 | 4 | `[3], [2,2], [4], [1], [4]` (5 days) | $5 > 3$, Impossible. `low = 5` |
| 4 | 5 | `[3,2], [2], [4,1], [4]` (4 days) | $4 > 3$, Impossible. `low = 6` |

**Result:** `6`

---

## Edge Cases

- `days = 1`: Answer is always `sum(weights)`.
- `days = len(weights)`: Answer is always `max(weights)`.
- All weights are equal: Range is smaller but logic remains identical.
- Single package: Answer is the weight of that package.

---

## Mistakes

- **Range Error:** Starting `low` at `1` or `0` instead of `max(weights)`. A capacity smaller than the heaviest item is never valid.
- **Greedy Reset:** Forgetting to reset `current_load` to the current weight `w` when a new day starts.
- **Off-by-one:** Initializing `days_needed` to `0` instead of `1`.
- **User Mistake:** No specific note provided. (Ensure you define the search space correctly even when no specific mistake is logged).

---

## Complexity

Time: $O(N \log(\sum \text{weights}))$ → Binary search takes $\log(\text{Range})$ steps; each step validates via $O(N)$ pass.  
Space: $O(1)$ → Only a few variables used for pointers and counters.

---

## Similar Problems

- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium
- [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #binary-search-on-answer #greedy
- [[Binary Search]] [[Greedy]]
- **Revision Date:** 2026-04-11
- **Problem Link:** [LeetCode 1011](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Meta #Microsoft #Apple #TikTok

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #greedy [[Greedy]], #search-space [[Search Space Optimization]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
