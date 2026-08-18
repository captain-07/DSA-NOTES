---
created: 2026-04-18
revisions:
  - 2026-04-20
  - 2026-04-25
  - 2026-05-03
  - 2026-05-18
---

# Painters Partition

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Adobe #Flipkart #Directi

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #greedy [[Greedy]]
  - #arrays [[Arrays]]

## Pattern

Binary Search on Answer (Minimize the Maximum value)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The answer lies in a monotonic range: `[max(boards), sum(boards)]`. If we can paint all boards within time `T` using `K` painters, we can also do it for any time `> T`. This monotonicity allows us to Binary Search for the minimum possible `T`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Search Space:** `low = max(arr)`, `high = sum(arr)`.
- **Greedy Check:** If `current_sum + board > mid`, increment `painter_count` and reset `current_sum`.
- **Opposite Polarity:** After `while low <= high` terminates, `high` is in the "Impossible" zone and `low` is in the "Possible" zone (the answer).

---

## Approach

### Brute Force
- Linear search from `max(boards)` to `sum(boards)`. For each value, check feasibility.
- **Time:** $O(N \times (\text{sum} - \text{max}))$

### Optimal
1. **Define Range:** The minimum possible time is the longest board (one painter takes it), and the maximum is the sum of all boards (one painter does everything).
2. **Binary Search:** Pick `mid`.
3. **Check Function:** Greedily assign boards to painters. If a painter exceeds `mid`, call the next painter.
4. **Adjust Range:**
   - If `painters_needed > k`: `mid` is too small, `low = mid + 1`.
   - If `painters_needed <= k`: `mid` is feasible, try smaller, `high = mid - 1`.
5. **Result:** Return `low`.

---

## Code (Python)

```python
class Solution:
    def paint(self, k: int, t: int, boards: list[int]) -> int:
        # t is time per unit; usually 1 in standard problems
        boards = [b * t for b in boards]
        
        def is_feasible(limit):
            painters = 1
            current_work = 0
            for board in boards:
                if current_work + board <= limit:
                    current_work += board
                else:
                    painters += 1
                    current_work = board
            return painters <= k

        low = max(boards)
        high = sum(boards)
        ans = high

        while low <= high:
            mid = (low + high) // 2
            if is_feasible(mid):
                ans = mid
                high = mid - 1 # Try to find a smaller maximum
            else:
                low = mid + 1 # Need more time to reduce painters
        
        return ans % 10000003 # Return low or ans (common constraints)
```

---

## Dry Run (Smart Example)

Input: `boards = [10, 20, 30, 40]`, `k = 2`
Range: `low = 40`, `high = 100`

| Step | Low | High | Mid | Painters Needed (Check) | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 40 | 100 | 70 | 2 ( {10,20,30}, {40} ) | `ans=70, high=69` |
| 2 | 40 | 69 | 54 | 3 ( {10,20}, {30}, {40} ) | `low=55` |
| 3 | 55 | 69 | 62 | 2 ( {10,20,30}, {40} ) | `ans=62, high=61` |
| 4 | 55 | 61 | 58 | 3 ( {10,20}, {30}, {40} ) | `low=59` |
| 5 | 59 | 61 | 60 | 2 ( {10,20,30}, {40} ) | `ans=60, high=59` |

**Termination:** `low (60) > high (59)`. Return `low` or `ans` = **60**.

---

## Edge Cases

- `k = 1`: Answer is `sum(boards)`.
- `k >= n`: Answer is `max(boards)` (each board gets its own painter).
- All boards same length: Simple division/multiple check.

---

## Mistakes

- **Comparison Logic:** `if painters > k` means the time limit `mid` is **too strict**. We must increase the time: `low = mid + 1`.
- **Returning `low` vs `high`:** 
  - At the start: `low` is in the **False** (Impossible) region, `high` is in the **True** (Possible) region.
  - By the end, they swap (Opposite Polarity). `high` ends at the largest "Impossible" value, and `low` ends at the smallest "Possible" value.
  - **Answer is `low`** because we want the *minimum* value that satisfies the condition.
- **Initialization:** `low` must be `max(arr)`, not `0`. You cannot paint a board of length 10 with a limit of 5.

---

## Complexity

Time: $O(N \log(\sum \text{boards}))$ → Binary search takes $\log(\text{Range})$, feasibility check takes $O(N)$.  
Space: $O(1)$ → No extra space used.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Allocate Books](https://www.interviewbit.com/problems/allocate-books/) - Medium
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #minimax #greedy
  - [[Binary Search]] [[Greedy]]
  - Revision Date: 2026-04-18
  - **Problem Link:** [Painters Partition Problem - GFG](https://www.geeksforgeeks.org/problems/the-painters-partition-problem1535/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-20)
- [ ] Day 7 Revision (2026-04-25)
- [ ] Day 15 Revision (2026-05-03)
- [ ] Day 30 Revision (2026-05-18)
