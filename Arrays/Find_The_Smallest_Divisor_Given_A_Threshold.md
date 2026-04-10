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
  - #Amazon #Google #Microsoft #Facebook #Uber #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Arrays]], #math [[Mathematics]]

## Pattern

Binary Search on Answer (Monotonic Function)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- The relationship between the **divisor** and the **resultant sum** is monotonic: as the divisor increases, the sum of divisions decreases.
- This allows us to binary search for the smallest divisor in the range `[1, max(nums)]` that satisfies the condition `sum(ceil(num / divisor)) <= threshold`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Range: `[1, max(nums)]`. 
- If `total_sum <= threshold`, the divisor might be smaller (search left); else, it must be larger (search right).

---

## Approach

### Brute Force
- Iterate through every possible divisor starting from 1 up to `max(nums)`. Calculate the sum for each and return the first one that satisfies the threshold.
- Time: $O(max(nums) \cdot N)$

### Optimal
- **Binary Search on Answer:**
  1. Define search space: `low = 1`, `high = max(nums)`.
  2. While `low <= high`:
     - Calculate `mid`.
     - Compute `total_sum = sum(ceil(n / mid))` for all `n` in `nums`.
     - If `total_sum <= threshold`, store `mid` as a potential answer and try smaller divisors (`high = mid - 1`).
     - Otherwise, try larger divisors (`low = mid + 1`).
- Time: $O(N \log(max(nums)))$

---

## Code (Python)

```python
import math

class Solution:
    def smallestDivisor(self, nums: list[int], threshold: int) -> int:
        # Range for binary search: 1 to the largest element in nums
        low, high = 1, max(nums)
        ans = high
        
        while low <= high:
            mid = (low + high) // 2
            
            # Calculate sum of ceil(num / mid)
            # Using (num + mid - 1) // mid is a faster way to compute ceil
            current_sum = sum((num + mid - 1) // mid for num in nums)
            
            if current_sum <= threshold:
                # Potential answer found, try to find a smaller divisor
                ans = mid
                high = mid - 1
            else:
                # Sum too large, need a larger divisor to decrease the sum
                low = mid + 1
                
        return ans
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 5, 9]`, `threshold = 6`

| Step | Low | High | Mid | Current Sum | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 9 | 5 | $1+1+1+2 = 5$ | $5 \le 6$. Potential ans = 5. Search left. |
| 2 | 1 | 4 | 2 | $1+1+3+5 = 10$ | $10 > 6$. Search right. |
| 3 | 3 | 4 | 3 | $1+1+2+3 = 7$ | $7 > 6$. Search right. |
| 4 | 4 | 4 | 4 | $1+1+2+3 = 7$ | $7 > 6$. Search right. |
| End | 5 | 4 | - | - | Result = 5 |

---

## Edge Cases

- **Threshold equals length of nums:** The smallest divisor will be `max(nums)`.
- **Threshold is very large:** The smallest divisor will likely be 1.
- **Single element array:** Binary search still applies; result is `ceil(nums[0] / threshold)`.
- **All elements are the same:** Simplifies the sum calculation but binary search remains robust.

---

## Mistakes

- Using `math.ceil(num / mid)` can be slow in some environments; `(num + mid - 1) // mid` is the integer math trick for ceiling.
- Incorrect binary search boundaries: the minimum divisor must be 1, not 0.
- User mistake: No specific note provided.

---

## Complexity

Time: $O(N \cdot \log(\max(nums)))$  
→ We perform binary search over the range of values in `nums`, and for each step, we iterate through the array once.

Space: $O(1)$  
→ No extra space used except for a few variables.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #monotonic #optimization
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
