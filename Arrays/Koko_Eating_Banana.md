---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Koko Eating Banana

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Netflix #Airbnb #Uber #DoorDash

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #monotonic [[Monotonic Function]]

## Pattern

Binary Search on Answer Range

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The total time taken is a **monotonically decreasing function** of the eating speed `k`. If Koko can finish all bananas at speed `k`, she can also finish them at any speed `k' > k`. This allows us to binary search for the minimum `k` in the range `[1, max(piles)]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the smallest `k` such that `sum(ceil(pile / k)) <= h`. Use Binary Search on the range of possible speeds.

---

## Approach

### Brute Force
- Try every speed `k` starting from 1 until Koko can finish within `h` hours.
- **Time Complexity:** O(max(P) * N) where N is number of piles.

### Optimal
- Use Binary Search on the range `[1, max(piles)]`.
- For a mid speed, calculate total hours required.
- If `total_hours <= h`, mid is a potential answer; try smaller speeds (left half).
- Else, speed is too slow; try larger speeds (right half).
- **Time Complexity:** O(N * log(max(P)))

---

## Code (Python)

```python
import math

class Solution:
    def minEatingSpeed(self, piles: list[int], h: int) -> int:
        # Range of possible eating speeds
        low, high = 1, max(piles)
        ans = high
        
        while low <= high:
            mid = (low + high) // 2
            
            # Calculate total hours needed at speed 'mid'
            total_hours = 0
            for pile in piles:
                total_hours += math.ceil(pile / mid)
            
            # If within time limit, record answer and try slower speed
            if total_hours <= h:
                ans = mid
                high = mid - 1
            else:
                # Need to eat faster
                low = mid + 1
                
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `piles = [3, 6, 7, 11]`, `h = 8`

| Step | Range [L, H] | Mid (Speed) | Total Hours Calculation | Result |
| :--- | :--- | :--- | :--- | :--- |
| 1 | [1, 11] | 6 | ceil(3/6)+ceil(6/6)+ceil(7/6)+ceil(11/6) = 1+1+2+2 = 6 | 6 <= 8 (Valid, Ans=6, H=5) |
| 2 | [1, 5] | 3 | ceil(3/3)+ceil(6/3)+ceil(7/3)+ceil(11/3) = 1+2+3+4 = 10 | 10 > 8 (Too slow, L=4) |
| 3 | [4, 5] | 4 | ceil(3/4)+ceil(6/4)+ceil(7/4)+ceil(11/4) = 1+2+2+3 = 8 | 8 <= 8 (Valid, Ans=4, H=3) |
| 4 | [4, 3] | - | Loop terminates | **Ans = 4** |

---

## Edge Cases

- `h == len(piles)`: Koko must eat at `max(piles)` speed.
- `len(piles) == 1`: Simple math `ceil(pile / h)`.
- `max(piles)` is very large: Binary search handles this efficiently.
- `h` is significantly larger than `sum(piles)`: Koko can eat at speed 1.

---

## Mistakes

- Using `(low + high) / 2` without considering integer division or overflow (though Python handles overflow).
- Forgetting to use `math.ceil` or equivalent integer math `(pile + mid - 1) // mid`.
- Setting `high` to `sum(piles)` instead of `max(piles)` (correct but less efficient).
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(N * log(M)) → Where N is the number of piles and M is the maximum number of bananas in a pile.  
Space: O(1) → We only use a few variables for binary search.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium
- [Heaters](https://leetcode.com/problems/heaters/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #leetcode
  - [[Binary Search]] [[Monotonic Function]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Koko Eating Banana](https://leetcode.com/problems/koko-eating-bananas/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
