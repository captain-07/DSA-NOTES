---
created: 2026-04-08
revisions:
  - 2026-04-10
  - 2026-04-15
  - 2026-04-23
  - 2026-05-08
---

# Minimum Number Of Days To Make M Bouquets

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Bloomberg #Microsoft #Directi

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #greedy [[Greedy]]
  - #arrays [[Arrays]]

## Pattern

Binary Search on Answer (Range Search)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The possible number of days ranges from `min(bloomDay)` to `max(bloomDay)`. Since the ability to make bouquets is **monotonic** (if you can make them on day $D$, you can also make them on $D+1$), we can binary search for the minimum day.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `m * k > len(bloomDay)`, return -1. Binary search the answer space; in each step, use a greedy linear scan to count adjacent flowers that have bloomed by `mid` days.

---

## Approach

### Brute Force
- Check every possible day from $1$ to $\max(bloomDay)$. For each day, count if $m$ bouquets can be formed.
- **Time Complexity:** $O(\max(bloomDay) \times N)$

### Optimal
- **Range:** $low = \min(bloomDay)$, $high = \max(bloomDay)$.
- **Binary Search:** Calculate `mid`. Check if `m` bouquets are possible on `mid` day.
- **Check Function:** Iterate through `bloomDay`. If `flower <= mid`, increment `count`. When `count == k`, increment `bouquets` and reset `count`.
- **Logic:** If `bouquets >= m`, `mid` is a potential answer; try smaller days (`high = mid - 1`). Otherwise, increase days (`low = mid + 1`).
- **Time Complexity:** $O(N \log(\max - \min))$

---

## Code (Python)

```python
def minDays(bloomDay, m, k):
    # Impossible case: not enough total flowers
    if m * k > len(bloomDay):
        return -1
    
    def canMake(day):
        bouquets = 0
        count = 0
        for flower in bloomDay:
            if flower <= day:
                count += 1
                if count == k:
                    bouquets += 1
                    count = 0
            else:
                count = 0 # Reset if flowers are not adjacent
        return bouquets >= m

    low, high = min(bloomDay), max(bloomDay)
    ans = high
    
    while low <= high:
        mid = (low + high) // 2
        if canMake(mid):
            ans = mid
            high = mid - 1
        else:
            low = mid + 1
            
    return ans
```

---

## Dry Run (Smart Example)

Input: `bloomDay = [7, 7, 7, 7, 12, 7, 7]`, `m = 2`, `k = 3`

| Step | low | high | mid | bouquets (canMake) | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 7 | 12 | 9 | `[7,7,7,7,X,7,7]` -> (1+1) = 2 | `ans=9`, `high=8` |
| 2 | 7 | 8 | 7 | `[7,7,7,7,X,7,7]` -> (1+1) = 2 | `ans=7`, `high=6` |
| 3 | 7 | 6 | - | Loop terminates | Result = 7 |

---

## Edge Cases

- **Total flowers < m * k:** Immediate return -1.
- **k = 1:** Each flower is a bouquet; reduces to finding the $m$-th smallest bloom day.
- **m = 1:** Finding the minimum day to get $k$ consecutive flowers.
- **All flowers bloom on the same day:** Answer is that day or -1.

---

## Mistakes

- **Initial Check:** Forgetting to check `m * k > n` leads to infinite loops or incorrect range logic.
- **Reset Logic:** Forgetting to reset the `count` to 0 when a flower hasn't bloomed yet (breaks adjacency).
- **Lower Bound:** Starting `low` at 0 instead of `min(bloomDay)` (minor optimization, but good for interviews).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(N \log(\text{max\_bloom\_day}))$ → Binary search takes $\log(\text{Range})$ steps, each with an $O(N)$ check.  
Space: $O(1)$ → Only a few variables used for tracking.

---

## Similar Problems

- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Greedy]]
- **Revision Date:** 2026-04-08
- **Problem Link:** [LeetCode - Minimum Number of Days to Make M Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-10)
- [ ] Day 7 Revision (2026-04-15)
- [ ] Day 15 Revision (2026-04-23)
- [ ] Day 30 Revision (2026-05-08)
