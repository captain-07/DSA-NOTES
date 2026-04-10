---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Capacity To Ship Packages Within D Days

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Meta #Microsoft #Flipkart #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #greedy [[Greedy]]
  - #arrays [[Arrays]]

---
## Pattern

Binary Search on Answer (Monotonic Range)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The required capacity has a **monotonic property**: If a capacity $X$ can ship all packages within $D$ days, any capacity $Y > X$ will also work. This allows us to binary search for the minimum valid capacity within the range `[max(weights), sum(weights)]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary Search on the **answer range**. Use a greedy helper function `canShip(capacity)` to count the number of days needed and adjust the search space.

---

## Approach

### Brute Force
- Try every possible capacity starting from `max(weights)` up to `sum(weights)` one by one.
- **Time Complexity:** $O(N \cdot \text{sum}(W))$

### Optimal
1. **Define Range:** Lower bound `low = max(weights)` (must carry the heaviest item), upper bound `high = sum(weights)` (can carry all in 1 day).
2. **Binary Search:** Calculate `mid` as current capacity.
3. **Validation:** Check if `mid` capacity is sufficient using a greedy pass.
   - If `canShip(mid) <= days`, `mid` might be the answer; try smaller (`high = mid`).
   - Else, capacity is too small; try larger (`low = mid + 1`).
4. **Result:** `low` will converge to the minimum required capacity.

---

## Code (Python)

```python
class Solution:
    def shipWithinDays(self, weights: list[int], days: int) -> int:
        def can_ship(capacity: int) -> bool:
            day_count = 1
            current_load = 0
            for w in weights:
                if current_load + w > capacity:
                    day_count += 1
                    current_load = 0
                current_load += w
            return day_count <= days

        # Range for Binary Search
        low, high = max(weights), sum(weights)
        ans = high
        
        while low <= high:
            mid = (low + high) // 2
            if can_ship(mid):
                ans = mid
                high = mid - 1 # Try to find a smaller valid capacity
            else:
                low = mid + 1 # Need more capacity
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `weights = [3,2,2,4,1,4], days = 3`  
**Range:** `low = 4`, `high = 16`

| Step | Mid (Cap) | Greedy Partitioning | Days Used | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | [3,2,2], [4,1,4] | 2 | `ans=10, high=9` |
| 2 | 6 | [3,2], [2,4], [1,4] | 3 | `ans=6, high=5` |
| 3 | 4 | [3], [2,2], [4], [1,4] | 4 | `low=5` |
| 4 | 5 | [3,2], [2], [4,1], [4] | 4 | `low=6` |

**Result:** 6

---

## Edge Cases

- `days = 1`: Answer is always `sum(weights)`.
- `days = len(weights)`: Answer is always `max(weights)`.
- All weights are identical: Uniform distribution across days.
- Single item in `weights`: Answer is that item's weight.

---

## Mistakes

- **Range Error:** Starting `low` at 1 or 0 instead of `max(weights)`. (Cannot ship an item heavier than capacity).
- **Greedy Logic:** Starting `day_count` at 0 instead of 1.
- **Binary Search:** Using `low < high` without proper handling of the boundary, leading to infinite loops.
- **User mistake:** No specific note provided.

---

## Complexity

Time: $O(N \cdot \log(\text{sum}(W) - \text{max}(W)))$ → Linear pass for every binary search step.  
Space: $O(1)$ → Only a few pointers/variables used.

---

## Similar Problems

- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium
- [Allocate Minimum Number of Pages](https://www.geeksforgeeks.org/allocate-minimum-number-pages/) - Hard

---

## Tags and Properties
- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Greedy]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [LeetCode - Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
