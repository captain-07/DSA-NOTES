---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

This is a structured Obsidian-ready note for the problem **Koko Eating Bananas**.

---

# 🍌 Koko Eating Bananas

---
### 📋 Properties
- **Difficulty:** #Medium 
- **Pattern:** #BinarySearchOnAnswer 
- **LeetCode:** [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
- **Last Reviewed:** 2026-04-11

---

## 🧩 Key Idea
The core insight is that the eating speed $k$ has a monotonic property: if Koko can finish all bananas at speed $k$, she can also finish them at any speed $> k$. This allows us to **Binary Search** over the range of possible speeds $[1, \max(piles)]$ to find the minimum $k$ that satisfies the time constraint $h$.

## 🚀 Approach
1. **Define the Search Space:** 
   - The minimum possible speed is **1** (she must eat at least one banana per hour).
   - The maximum speed she ever needs is **$\max(piles)$** (eating the largest pile in exactly one hour).
2. **Binary Search Logic:**
   - Pick a middle speed `mid`.
   - Calculate the total hours required to eat all piles at speed `mid`.
   - To calculate hours for a pile $p$: $\lceil p / mid \rceil$ (which is `(p + mid - 1) // mid` in integer math).
3. **Decision Rule:**
   - If `total_hours <= h`: Koko is eating fast enough. This *could* be the answer, but there might be a slower speed that also works. Store `mid` as the current best answer and search the **left** half (`high = mid - 1`).
   - If `total_hours > h`: Koko is eating too slowly. She needs to speed up. Search the **right** half (`low = mid + 1`).

## 💻 Code
```python
import math

class Solution:
    def minEatingSpeed(self, piles: list[int], h: int) -> int:
        # Step 1: Initialize the range for Binary Search
        low = 1
        high = max(piles)
        ans = high
        
        while low <= high:
            mid = low + (high - low) // 2
            
            # Step 2: Check if speed 'mid' is feasible
            total_hours = 0
            for p in piles:
                # Ceiling division: math.ceil(p / mid)
                total_hours += (p + mid - 1) // mid
            
            # Step 3: Shrink the search space
            if total_hours <= h:
                ans = mid  # Potential answer found
                high = mid - 1
            else:
                low = mid + 1
                
        return ans
```

## 🏗️ Pattern
> [!IMPORTANT]
> **Binary Search on Answer**
> This pattern is used when you are asked to find a "minimum" or "maximum" value $X$ such that a condition is met, and the condition is **monotonic** (if it works for $X$, it works for all values larger/smaller than $X$).

## 🏃 Dry Run
**Input:** `piles = [3, 6, 7, 11]`, `h = 8`
- `low = 1`, `high = 11`
- `mid = 6`: Hours = $\lceil 3/6 \rceil + \lceil 6/6 \rceil + \lceil 7/6 \rceil + \lceil 11/6 \rceil = 1 + 1 + 2 + 2 = 6$. 
  - $6 \le 8$ (True). `ans = 6`, `high = 5`.
- `mid = 3`: Hours = $1 + 2 + 3 + 4 = 10$. 
  - $10 > 8$ (False). `low = 4`.
- `mid = 4`: Hours = $1 + 2 + 2 + 3 = 8$. 
  - $8 \le 8$ (True). `ans = 4`, `high = 3`.
- Loop ends. **Result: 4**.

## ⚠️ Edge Cases
- **$h = \text{len}(piles)$**: Koko must eat at a speed equal to the maximum pile size to finish exactly on time.
- **$h$ is very large**: Koko can eat at speed 1.
- **Single pile**: The speed will be $\lceil \text{pile} / h \rceil$.

## 💡 Mistakes
> [!WARNING]
> **Common Pitfall:** Using `math.ceil(p / mid)` can sometimes lead to precision issues with very large floating-point numbers in some languages. 
> **Correction:** Use integer-based ceiling division: `(p + mid - 1) // mid`.
> 
> **Range Error:** Don't set `high` to the sum of all bananas. While safe, it makes the search space unnecessarily large ($10^{14}$ vs $10^9$). The max speed required is always $\max(piles)$.

## 📊 Complexity
- **Time Complexity:** $O(N \cdot \log(\max(P)))$ where $N$ is the number of piles and $P$ is the max pile size.
- **Space Complexity:** $O(1)$ as we only use a few variables.

## 🏆 Difficulty
**Medium**

## 📎 Metadata & Placement Tags
#dsa #binary-search #leetcode #blind75

## 🔗 Similar Problems
- [1011. Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
- [1482. Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/)
- [1283. Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
