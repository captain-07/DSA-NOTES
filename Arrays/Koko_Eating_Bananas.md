---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Koko Eating Bananas

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Airbnb #Amazon #Google #Netflix #Microsoft

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #math [[Ceiling Division]]

## Pattern

Binary Search on Answer Range

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The possible eating speed $k$ ranges from **1** to **max(piles)**. Since the total time spent eating is **monotonically decreasing** as $k$ increases, we can binary search for the minimum $k$ that satisfies the condition `total_hours <= h`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary search the **speed** (1 to max pile). For each `mid`, calculate total hours using `ceil(pile / mid)`. If hours $\le$ $H$, it's a candidate; try smaller.

---

## Approach

### Brute Force
- Check every possible speed $k$ starting from 1 up to `max(piles)`.
- **Time Complexity:** $O(N \times M)$ where $N$ is number of piles and $M$ is the maximum bananas in a pile.

### Better
- *N/A - The transition from linear search to binary search is the standard jump for this problem.*

### Optimal (Binary Search on Answer)
1. Initialize `low = 1`, `high = max(piles)`.
2. While `low <= high`:
   - Calculate `mid` (current speed).
   - Calculate `total_hours = sum(math.ceil(pile / mid) for pile in piles)`.
   - If `total_hours <= h`: `mid` is a potential answer, store it and try a slower speed (`high = mid - 1`).
   - Else: Speed is too slow, try a faster speed (`low = mid + 1`).
3. Return the smallest valid `mid` found.

---

## Code (Python)

```python
import math

def minEatingSpeed(piles, h):
    # Search space: minimum speed is 1, maximum is the largest pile
    low, high = 1, max(piles)
    res = high
    
    while low <= high:
        k = (low + high) // 2
        total_hours = 0
        
        # Calculate hours needed for speed k
        for p in piles:
            total_hours += math.ceil(p / k)
        
        if total_hours <= h:
            res = k          # Valid speed, but can we go slower?
            high = k - 1
        else:
            low = k + 1      # Too slow, must eat faster
            
    return res
```

---

## Dry Run (Smart Example)

**Input:** `piles = [3, 6, 7, 11]`, `h = 8`

| Step | Low | High | Mid (k) | Total Hours Calculation | Total | Condition (Total <= 8) | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 11 | 6 | ceil(3/6)+ceil(6/6)+ceil(7/6)+ceil(11/6) = 1+1+2+2 | 6 | Yes | res=6, high=5 |
| 2 | 1 | 5 | 3 | ceil(3/3)+ceil(6/3)+ceil(7/3)+ceil(11/3) = 1+2+3+4 | 10 | No | low=4 |
| 3 | 4 | 5 | 4 | ceil(3/4)+ceil(6/4)+ceil(7/4)+ceil(11/4) = 1+2+2+3 | 8 | Yes | res=4, high=3 |
| 4 | 4 | 3 | - | Loop terminates (low > high) | - | - | Return 4 |

---

## Edge Cases

- **h == len(piles):** Koko must eat at a speed equal to `max(piles)`.
- **Single pile:** The answer is simply `math.ceil(piles[0] / h)`.
- **Large h:** If `h` is very large, Koko can eat at speed 1.
- **Max pile size:** The result will never exceed the maximum value in `piles`.

---

## Mistakes

- **Linear Search:** Counting the hour for each possible answer from 1 to max pile size ($O(N \cdot M)$).
- **Integer Division:** Forgetting to use `ceil` or `(p + k - 1) // k` for integer-only ceiling division.
- **Binary Search Range:** Starting `low` at 0 (division by zero error) instead of 1.
- **Condition Logic:** Moving `low` when it should be `high` (mixing up the relationship between speed and time).

---

## Complexity

Time: $O(N \cdot \log(\max(\text{piles})))$ → We binary search over a range of size $M$, doing $O(N)$ work at each step.  
Space: $O(1)$ → No extra data structures used besides a few variables.

---

## Tags and Properties
- #dsa #important #revisit #binarysearch [[Binary Search]] #arrays [[Arrays]]
- **Revision Date:** 2026-04-07
- **Related:** [[Search in Rotated Sorted Array]], [[Find Minimum in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
