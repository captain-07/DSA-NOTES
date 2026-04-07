---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Koko Eating Banana

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Airbnb #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern
Binary Search on Answer (Range Search)

---
## Difficulty
Medium #medium

---

## ⚡ Key Idea (Core Insight)
The possible eating speed `k` lies in a predictable range: `[1, max(piles)]`. If Koko can finish all bananas at speed `k` within `h` hours, she can also finish them at any speed `> k`. This monotonicity allows us to use **Binary Search** to find the minimum `k`.

---

## ⚡ Quick Recall (VERY IMPORTANT)
Binary search for the smallest speed `k` in range `[1, max(piles)]` where the total hours calculated as `sum(ceil(pile/k))` is less than or equal to `h`.

---

## Approach

### Brute Force
- Iterate through every possible speed `k` starting from 1 up to `max(piles)`. For each `k`, calculate the total hours needed. The first `k` that satisfies `total_hours <= h` is the answer.
- **Time Complexity:** O(N * M), where N is `len(piles)` and M is `max(piles)`.

### Optimal
1. **Define Range:** The minimum possible speed is 1, and the maximum is `max(piles)` (eating the largest pile in one hour).
2. **Binary Search:** Perform binary search on the range `[low, high]`.
3. **Check Condition:** For a candidate speed `mid`, calculate total hours: `sum((p + mid - 1) // mid for p in piles)`.
4. **Shrink Range:**
   - If `total_hours <= h`, then `mid` is a possible answer. Try to find a smaller speed by searching in the left half (`high = mid - 1`).
   - If `total_hours > h`, the speed is too slow. Search in the right half (`low = mid + 1`).
- **Time Complexity:** O(N * log(M)).

---

## Code (Python)

```python
import math

def minEatingSpeed(piles, h):
    # Search space for speed k
    low, high = 1, max(piles)
    ans = high
    
    while low <= high:
        mid = (low + high) // 2
        
        # Calculate total hours spent at speed 'mid'
        total_hours = 0
        for p in piles:
            # (p + mid - 1) // mid is an integer way to do math.ceil(p / mid)
            total_hours += (p + mid - 1) // mid
            
        if total_hours <= h:
            # Found a valid speed, record and try to find a smaller one
            ans = mid
            high = mid - 1
        else:
            # Speed is too slow, must increase it
            low = mid + 1
            
    return ans
```

---

## Dry Run (Smart Example)
**Input:** `piles = [3, 6, 7, 11]`, `h = 8`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `low=1, high=11, mid=6` | Hours: `1+1+2+2 = 6`. `6 <= 8` is True. `ans=6, high=5`. |
| 2 | `low=1, high=5, mid=3` | Hours: `1+2+3+4 = 10`. `10 <= 8` is False. `low=4`. |
| 3 | `low=4, high=5, mid=4` | Hours: `1+2+2+3 = 8`. `8 <= 8` is True. `ans=4, high=3`. |
| 4 | `low=4, high=3` | `low > high`, loop terminates. Return `ans = 4`. |

---

## Edge Cases

- `h == len(piles)`: Koko must eat at a speed equal to the largest pile size to finish on time.
- `len(piles) == 1`: Simple range search where `ans = ceil(pile / h)`.
- `h` is extremely large: The speed will be 1 as it's the minimum possible.
- All piles are the same size: Binary search still efficiently finds the boundary.

---

## Mistakes

- **Integer Division:** Forgetting to use `math.ceil()` or the `(p + k - 1) // k` trick, leading to incorrect hour counts.
- **Search Range:** Using `sum(piles)` as the upper bound (unnecessary and slower) instead of `max(piles)`.
- **Binary Search Condition:** Using `low < high` instead of `low <= high` without proper adjustment of `ans`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N * log(M)) → We check `N` piles for each step of the binary search over range `M` (`max(piles)`).  
Space: O(1) → Constant space for pointers and temporary calculations.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #koko-eating-banana #monotonicity  
  - [[Binary Search]] [[Arrays]]
  - Revision Date: 2026-04-07
  - **Problem Link:** [LeetCode - Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
