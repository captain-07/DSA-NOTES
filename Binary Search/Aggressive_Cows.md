---
created: 2026-04-13
revisions:
  - 2026-04-15
  - 2026-04-20
  - 2026-04-28
  - 2026-05-13
---

# Aggressive Cows

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Zomato #Paytm #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binary-search [[Binary Search]]
  - #sorting [[Sorting]]
  - #greedy [[Greedy]]

---
## Pattern

Binary Search on Answer (Maximize the Minimum)

---
## Difficulty

Medium  
#medium

---
## ⚡ Key Idea (Core Insight)

The problem asks to **maximize the minimum distance**. Since the possible distance range $[1, \text{max\_pos} - \text{min\_pos}]$ is monotonic (if a distance $d$ is possible, all distances $< d$ are also possible), we use **Binary Search on the distance**. For each mid-value, use a **Greedy** check to see if $K$ cows can be placed.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Sort stalls $\rightarrow$ Binary search on the *minimum gap* $\rightarrow$ Use a `canPlace` helper to greedily put cows in stalls only if `current_pos - last_pos >= gap`.

---
## Approach

### Brute Force
- Iterate through every possible distance $d$ from $1$ to $(\text{max} - \text{min})$. For each $d$, check if $k$ cows can be placed.
- **Time Complexity:** $O(\text{Range} \times N)$

### Optimal
- **Step 1:** Sort the stall positions to allow greedy placement.
- **Step 2:** Binary Search on the answer space: `low = 1`, `high = stalls[-1] - stalls[0]`.
- **Step 3:** In `is_possible(dist)`: Place the first cow at `stalls[0]`. Iterate through stalls and place the next cow only if the gap $\ge dist$.
- **Step 4:** If `is_possible` is true, move `low = mid + 1` (try larger distance); else move `high = mid - 1`.
- **Time Complexity:** $O(N \log N + N \log(\text{Range}))$

---
## Code (Python)

```python
class Solution:
    def solve(self, n, k, stalls):
        # Sorting is mandatory for greedy placement
        stalls.sort()
        
        def is_possible(dist):
            count = 1 # Place first cow at stalls[0]
            last_pos = stalls[0]
            
            for i in range(1, n):
                if stalls[i] - last_pos >= dist:
                    count += 1
                    last_pos = stalls[i]
            
            # Key check: Can we place at least k cows?
            return count >= k

        low = 1
        high = stalls[-1] - stalls[0]
        ans = 1
        
        while low <= high:
            mid = (low + high) // 2
            if is_possible(mid):
                ans = mid # Potential answer, try for more
                low = mid + 1
            else:
                high = mid - 1
                
        return ans
```

---
## Dry Run (Smart Example)

**Input:** `stalls = [1, 2, 8, 4, 9]`, `k = 3`  
**Sorted:** `[1, 2, 4, 8, 9]`, `low = 1`, `high = 8`

| Step | Low | High | Mid | `is_possible(mid)` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 8 | 4 | True | Place at [1, 8, 9] (Gap $\ge 4$). `ans = 4`. |
| 2 | 5 | 8 | 6 | False | Place at [1, 8]. Only 2 cows fit. |
| 3 | 5 | 5 | 5 | False | Place at [1, 8]. Only 2 cows fit. |
| 4 | 5 | 4 | - | Break | Final Answer: 4 |

---
## Edge Cases

- **k = 2:** Answer is always `stalls[-1] - stalls[0]`.
- **k = n:** Answer is the minimum gap between any two adjacent stalls.
- **Uniformly spaced stalls:** Binary search handles this naturally.
- **Large coordinates:** Handled by $O(\log \text{Range})$ complexity.

---
## Mistakes

- **Forgetting to sort:** Greedy check fails if stalls aren't in order.
- **Range selection:** `low` should be $1$ (or min gap), not $0$.
- **Helper Condition:** **User Mistake:** Always ensure you check `count >= k` in the helper function; checking `count == k` is insufficient as placing more is also valid for the distance.
- **Update Logic:** In `is_possible == True`, update `ans = mid` and move `low = mid + 1` to maximize.

---
## Complexity

- **Time:** $O(N \log N + N \log D)$ → $N \log N$ for sorting, $N \log D$ for Binary Search where $D = \text{max\_pos} - \text{min\_pos}$.  
- **Space:** $O(1)$ → Excluding sorting space, only pointers are used.

---
## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Allocate Minimum Number of Pages](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1) - Hard

---
## Tags and Properties
- #dsa #important #revisit #binarysearch #greedy
- [[Binary Search]] [[Greedy Algorithms]]
- **Problem Link:** [Aggressive Cows (Spoj)](https://www.spoj.com/problems/AGGRCOW/) | [GFG](https://www.geeksforgeeks.org/problems/aggressive-cows/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-15)
- [ ] Day 7 Revision (2026-04-20)
- [ ] Day 15 Revision (2026-04-28)
- [ ] Day 30 Revision (2026-05-13)
