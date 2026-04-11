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

Binary Search on Answer (Search Space: [max(weights), sum(weights)])

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- The minimum possible capacity is `max(weights)` (must carry the heaviest item) and the maximum is `sum(weights)` (carry all in one day).
- The "feasible" function is monotonic: if capacity $X$ works, any capacity $> X$ also works. This property allows **Binary Search on the Answer**.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Binary search the range `[max(weights), sum(weights)]`. Use a greedy helper function to count days needed for a fixed capacity.

---

## Approach

### Brute Force
- Try every capacity starting from `max(weights)` and increment by 1 until the packages can be shipped within `D` days.
- **Time Complexity:** $O(N \times \text{sum}(weights))$

### Optimal
- Use **Binary Search** on the capacity range `[low, high]`.
- For `mid` capacity, greedily pack items. If `days > D`, we need more capacity (`low = mid + 1`); otherwise, `mid` is a candidate, try smaller (`high = mid - 1`).
- **Time Complexity:** $O(N \log(\text{sum}(weights)))$

---

## Code (Python)

```python
class Solution:
    def shipWithinDays(self, weights: list[int], days: int) -> int:
        def can_ship(capacity: int) -> bool:
            # Greedily count days needed for this capacity
            needed_days = 1
            current_load = 0
            for w in weights:
                if current_load + w > capacity:
                    needed_days += 1
                    current_load = 0
                current_load += w
            return needed_days <= days

        # Search space for capacity
        low, high = max(weights), sum(weights)
        ans = high
        
        while low <= high:
            mid = (low + high) // 2
            if can_ship(mid):
                ans = mid
                high = mid - 1 # Try to find a smaller feasible capacity
            else:
                low = mid + 1 # Increase capacity
                
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `weights = [3, 2, 2, 4, 1, 4]`, `days = 3`  
**Range:** `low = 4 (max)`, `high = 16 (sum)`

| Step | mid (Cap) | Day Count Calculation | Result |
| :--- | :--- | :--- | :--- |
| 1 | 10 | [3,2,2], [4,1,4] → 2 Days | $\le 3$ (True), high = 9 |
| 2 | 6 | [3,2], [2,4], [1,4] → 3 Days | $\le 3$ (True), high = 5 |
| 3 | 4 | [3], [2,2], [4], [1], [4] → 5 Days | $> 3$ (False), low = 5 |
| 4 | 5 | [3,2], [2], [4,1], [4] → 4 Days | $> 3$ (False), low = 6 |

**Final Ans:** 6

---

## Edge Cases

- `days = 1`: Answer is always `sum(weights)`.
- `days = len(weights)`: Answer is always `max(weights)`.
- All weights are equal: Range is still valid; logic holds.
- Only one package: Capacity must be the weight of that package.

---

## Mistakes

- **Incorrect Search Space:** Starting `low` at 1 or 0 instead of `max(weights)` (capacity must at least accommodate the largest item).
- **Greedy Logic:** Forgetting to reset `current_load` to the current weight `w` when starting a new day (not 0).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N \log(\text{sum}(W) - \max(W)))$ → Binary search takes log of range, each step iterates weights.  
Space: $O(1)$ → Constant extra space used for pointers and greedy check.

---

## Similar Problems

- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium
- [Allocating Books](https://www.geeksforgeeks.org/allocate-minimum-number-pages/) - Hard

---

## Tags and Properties
- #dsa #important #revisit #binary-search-on-answer
- [[Binary Search]] [[Greedy]]
- **Revision Date:** 2026-04-11
- **Problem Link:** [LeetCode - Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Facebook #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #greedy [[Greedy]], #arrays [[Arrays]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
