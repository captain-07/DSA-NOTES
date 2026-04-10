---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Find The Smallest Divisor Given A Threshold

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Bloomberg #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #binarysearchonanswer [[Binary Search on Answer]]
  - #array [[Array]]

---
## Pattern

Binary Search on Answer (Monotonic Function)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- The sum of division results $f(d) = \sum \lceil nums[i] / d \rceil$ is **monotonically decreasing** as the divisor $d$ increases.
- If a divisor $d$ satisfies the threshold, any divisor $> d$ will also satisfy it; we need the **smallest** such $d$.
- The search space for the divisor is bounded between $[1, \max(nums)]$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Range [1, max(nums)] + `math.ceil(n/mid)` + Find first `True` in `FFFFTTTT` pattern.

---

## Approach

### Brute Force
- Iterate through every possible divisor $d$ from $1$ to $\max(nums)$.
- For each $d$, calculate the sum and return the first $d$ where sum $\le threshold$.
- **Time Complexity:** $O(n \times \max(nums))$

### Optimal
- **Binary Search on Answer:** Initialize `low = 1`, `high = max(nums)`.
- While `low <= high`:
    1. Pick `mid = (low + high) // 2`.
    2. Calculate `total_sum = sum(ceil(x/mid) for x in nums)`.
    3. If `total_sum <= threshold`: This is a possible answer; try smaller divisors by setting `high = mid - 1`.
    4. Else: Divisor is too small; set `low = mid + 1`.
- Return `low` (the smallest divisor).

---

## Code (Python)

```python
import math

class Solution:
    def smallestDivisor(self, nums: list[int], threshold: int) -> int:
        # Range of possible divisors
        low, high = 1, max(nums)
        ans = high
        
        while low <= high:
            mid = (low + high) // 2
            
            # Calculate sum of ceil(num / mid)
            # Efficient ceil: (num + mid - 1) // mid
            current_sum = sum((num + mid - 1) // mid for num in nums)
            
            if current_sum <= threshold:
                ans = mid # Potential answer found
                high = mid - 1 # Try to find a smaller divisor
            else:
                low = mid + 1 # Sum too large, need larger divisor
                
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 5, 9]`, `threshold = 6`

| Step | Low | High | Mid | `current_sum` Calculation | Sum | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 9 | 5 | $1+1+1+2$ | 5 | $5 \le 6 \rightarrow$ `ans=5`, `high=4` |
| 2 | 1 | 4 | 2 | $1+1+3+5$ | 10 | $10 > 6 \rightarrow$ `low=3` |
| 3 | 3 | 4 | 3 | $1+1+2+3$ | 7 | $7 > 6 \rightarrow$ `low=4` |
| 4 | 4 | 4 | 4 | $1+1+2+3$ | 7 | $7 > 6 \rightarrow$ `low=5` |
| **End** | **5** | **4** | - | - | - | **Return ans = 5** |

---

## Edge Cases

- `threshold == len(nums)`: Smallest divisor will be `max(nums)`.
- `threshold` is very large: Smallest divisor will be `1`.
- `nums` contains all same values: Search still works correctly.
- Single element in `nums`: Logic reduces to `ceil(nums[0]/mid) <= threshold`.

---

## Mistakes

- **Rounding Error:** Forgetting to use `ceil()` or the integer trick `(a + b - 1) // b`.
- **Search Space:** Starting `high` at `threshold` instead of `max(nums)`.
- **Efficiency:** Using `math.ceil(a/b)` which involves float conversion instead of integer math.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N \log(\max(nums)))$ → Binary search takes $\log(\max(nums))$ steps, each step iterates through $N$ elements.  
Space: $O(1)$ → Constant space used for pointers and sum.

---

## Similar Problems

- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium
- [Heaters](https://leetcode.com/problems/heaters/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch
  - [[Binary Search]] [[Monotonic Function]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
