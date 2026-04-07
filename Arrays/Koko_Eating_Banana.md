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
  - #Amazon #Google #Microsoft #Netflix #Airbnb #DoorDash

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Array]]

---
## Pattern

Binary Search on Answer (Monotonic Search Space)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The possible eating speed $k$ ranges from $1$ (minimum) to $max(piles)$ (maximum needed to finish in $n$ hours). Since the total time taken is monotonically decreasing as $k$ increases, we can binary search for the minimum $k$ that satisfies the condition $total\_hours \le h$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary Search over speed range $[1, max(piles)]$. For each mid $k$, calculate total hours using $\sum \lceil pile/k \rceil$. If possible, shrink right; else, move left.

---

## Approach

### Brute Force
- Try every integer speed $k$ starting from 1 until the condition is met.
- **Time:** $O(max(P) \cdot N)$, where $P$ is the max pile size and $N$ is the number of piles.

### Optimal
1. Define search space: `left = 1`, `right = max(piles)`.
2. While `left <= right`:
   - Calculate `mid` (current speed $k$).
   - Calculate total hours: `sum((p + mid - 1) // mid for p in piles)`.
   - If `hours <= h`: This $k$ works; store it and try a smaller speed (`right = mid - 1`).
   - Else: Speed is too slow; increase it (`left = mid + 1`).
3. Return the stored result.

---

## Code (Python)

```python
import math

def minEatingSpeed(piles, h):
    # Search space for the speed k
    left, right = 1, max(piles)
    result = right
    
    while left <= right:
        k = left + (right - left) // 2
        
        # Calculate total hours needed at speed k
        # Equivalent to ceil(p/k)
        total_hours = 0
        for p in piles:
            total_hours += (p + k - 1) // k
            
        if total_hours <= h:
            # Possible speed, try to find a smaller one
            result = k
            right = k - 1
        else:
            # Too slow, must increase speed
            left = k + 1
            
    return result
```

---

## Dry Run (Smart Example)

**Input:** `piles = [3, 6, 7, 11], h = 8`

| Step | Range [L, R] | Mid (k) | Total Hours Calculation | Result | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | [1, 11] | 6 | $\lceil 3/6 \rceil + \lceil 6/6 \rceil + \lceil 7/6 \rceil + \lceil 11/6 \rceil = 1+1+2+2 = 6$ | 6 | $6 \le 8$, $R = 5$ |
| 2 | [1, 5] | 3 | $\lceil 3/3 \rceil + \lceil 6/3 \rceil + \lceil 7/3 \rceil + \lceil 11/3 \rceil = 1+2+3+4 = 10$ | 6 | $10 > 8$, $L = 4$ |
| 3 | [4, 5] | 4 | $\lceil 3/4 \rceil + \lceil 6/4 \rceil + \lceil 7/4 \rceil + \lceil 11/4 \rceil = 1+2+2+3 = 8$ | 4 | $8 \le 8$, $R = 3$ |
| 4 | [4, 3] | - | Loop terminates | 4 | Final Result |

---

## Edge Cases

- **len(piles) == h:** Minimum speed is exactly `max(piles)`.
- **h is very large:** Minimum speed will be 1 (Koko eats as slowly as possible).
- **Single Pile:** Result is `ceil(pile / h)`.
- **All piles same size:** Result is `ceil(pile_size / (h/n))`.

---

## Mistakes

- Using `p // k` instead of `ceil(p / k)` (integer division truncates).
- Setting the initial `right` boundary to an arbitrary large number (inefficient).
- Not using `(p + k - 1) // k` for integer-only ceiling division.
- **User Mistake:** No specific note provided.

---

## Complexity

- **Time:** $O(N \cdot \log(max(P)))$ → Binary search takes $\log(max(P))$ steps, and each step iterates through $N$ piles.
- **Space:** $O(1)$ → Only a few variables for pointers and sum.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) - Medium
- [Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Array]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [LeetCode 875 - Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
