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
  - #Amazon #Google #Microsoft #Uber #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]], #math [[Mathematics]]

---
## Pattern

Binary Search on Answer (Monotonic Objective Function)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The sum of divisions is **monotonically decreasing** as the divisor increases. If a divisor `X` satisfies the threshold, any divisor `Y > X` will also satisfy it. This allows us to use Binary Search to find the "First True" position (the smallest divisor) in the range `[1, max(nums)]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

When the result sum decreases as the variable increases, Binary Search the range of possible answers. Use `(num + divisor - 1) // divisor` for fast ceiling division.

---

## Approach

### Brute Force
- Iterate through every possible divisor from `1` to `max(nums)`. For each, calculate the sum and check against the threshold.
- **Time Complexity:** O(N * max(nums))

### Optimal
1. Define the search range: `low = 1`, `high = max(nums)`.
2. While `low <= high`, calculate `mid`.
3. Calculate the sum of `ceil(nums[i] / mid)`.
4. If `sum <= threshold`: `mid` is a candidate; try smaller divisors by setting `high = mid - 1`.
5. Else: `mid` is too small; set `low = mid + 1`.
6. Return `low`.

---

## Code (Python)

```python
import math

class Solution:
    def smallestDivisor(self, nums: list[int], threshold: int) -> int:
        # Range for binary search: 1 to the largest element in nums
        low, high = 1, max(nums)
        
        def calculate_sum(divisor: int) -> int:
            total_sum = 0
            for num in nums:
                # Efficient ceiling division: (a + b - 1) // b
                total_sum += (num + divisor - 1) // divisor
            return total_sum

        while low <= high:
            mid = low + (high - low) // 2
            
            if calculate_sum(mid) <= threshold:
                # Valid divisor, but look for a smaller one
                high = mid - 1
            else:
                # Sum too large, need a bigger divisor
                low = mid + 1
        
        return low
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 5, 9]`, `threshold = 6`

| Step | Range [L, R] | Mid | Sum Calculation | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | [1, 9] | 5 | 1+1+1+2 = **5** | $5 \le 6$. Valid. Search left: R = 4. |
| 2 | [1, 4] | 2 | 1+1+3+5 = **10** | $10 > 6$. Too small. Search right: L = 3. |
| 3 | [3, 4] | 3 | 1+1+2+3 = **7** | $7 > 6$. Too small. Search right: L = 4. |
| 4 | [4, 4] | 4 | 1+1+2+3 = **7** | $7 > 6$. Too small. Search right: L = 5. |

**Result:** `low = 5`

---

## Edge Cases

- **Threshold = len(nums):** The smallest divisor will be `max(nums)` because each element must be reduced to 1.
- **All nums same:** The sum becomes `len(nums) * ceil(val/divisor)`.
- **Large Threshold:** If threshold is very large, the divisor will likely be 1.
- **Single element array:** Binary search still works correctly on the single value range.

---

## Mistakes

- **Ceiling Division:** Using `round()` instead of `math.ceil()` or integer-based `(a+b-1)//b`.
- **Search Range:** Starting `high` at `sum(nums)` instead of `max(nums)` (inefficient but works) or starting at 0 (division by zero error).
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** O(N * log(M)) → Where N is the number of elements and M is the maximum value in `nums`.
- **Space:** O(1) → Only a few variables used for binary search.

---

## Similar Problems

- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #binarysearchonanswer
- [[Binary Search]] [[Math]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [LeetCode - Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
