---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Minimum Number Of Days To Make M Bouquets

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Bloomberg #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #greedy [[Greedy]], #array [[Array]]

## Pattern

Binary Search on Answer (Monotonic Function)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The problem exhibits a **monotonic property**: if it is possible to make $m$ bouquets on day $D$, it is definitely possible on any day $> D$. This allows us to binary search the answer in the range $[min(bloomDay), max(bloomDay)]$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Binary search for the "minimum day". For each mid-day, use a greedy sliding count to see if you can pick $k$ adjacent flowers $m$ times.

---

## Approach

### Brute Force
- Iterate through every possible day from $1$ to $10^9$ and check if $m$ bouquets can be formed.
- **Time Complexity:** $O(max(bloomDay) \times N)$

### Optimal
- **Binary Search on Answer:** Define a search space between the minimum and maximum bloom days.
- **Check Function:** In each step, iterate through `bloomDay`. Count contiguous flowers where `bloomDay[i] <= mid`. Every time the count reaches $k$, increment bouquets and reset the count.
- **Decision:** If bouquets $\ge m$, try a smaller day (move `high`); otherwise, increase the day (move `low`).
- **Time Complexity:** $O(N \log(max(bloomDay)))$

---

## Code (Python)

```python
class Solution:
    def minDays(self, bloomDay: list[int], m: int, k: int) -> int:
        # Edge case: Not enough flowers exist in total
        if m * k > len(bloomDay):
            return -1
        
        def can_make_bouquets(day: int) -> bool:
            bouquets = 0
            flowers = 0
            for bloom in bloomDay:
                if bloom <= day:
                    flowers += 1
                    if flowers == k:
                        bouquets += 1
                        flowers = 0
                else:
                    # Adjacency broken
                    flowers = 0
            return bouquets >= m

        low, high = min(bloomDay), max(bloomDay)
        ans = high
        
        while low <= high:
            mid = (low + high) // 2
            if can_make_bouquets(mid):
                ans = mid
                high = mid - 1
            else:
                low = mid + 1
                
        return ans
```

---

## Dry Run (Smart Example)

Input: `bloomDay = [7, 7, 7, 7, 12, 7, 7], m = 2, k = 3`

| Step | Low | High | Mid | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 7 | 12 | 9 | `can_make(9)`: Flowers $\le 9 \to [T, T, T, T, F, T, T]$. Bouquets: 1. `1 < 2` → False. |
| 2 | 10 | 12 | 11 | `can_make(11)`: Flowers $\le 11 \to [T, T, T, T, F, T, T]$. Bouquets: 1. `1 < 2` → False. |
| 3 | 12 | 12 | 12 | `can_make(12)`: Flowers $\le 12 \to [T, T, T, T, T, T, T]$. Bouquets: 2. `2 >= 2` → True. |
| 4 | 12 | 11 | - | Loop terminates. Result = 12. |

---

## Edge Cases

- **$m \times k > n$:** Return -1 immediately (not enough flowers).
- **$k = 1$:** The problem reduces to finding the $m$-th smallest unique bloom day.
- **$m = 1$:** Find the minimum day that has at least $k$ contiguous flowers.
- **All days same:** If $m \times k \le n$, the answer is simply the bloom day value.

---

## Mistakes

- **Greedy Reset:** Forgetting to reset the `flowers` counter to 0 when a flower hasn't bloomed yet (`bloom > day`).
- **Range Initialization:** Starting `low` at 0 or 1 instead of `min(bloomDay)` (minor optimization, but 0 can lead to errors).
- **Overflow:** (Not applicable in Python) In C++/Java, `m * k` can overflow an integer.
- **User mistake:** No specific note provided.

---

## Complexity

Time: $O(N \log(D))$ → where $N$ is array length and $D$ is the range of bloom days.  
Space: $O(1)$ → No extra data structures used beyond variables.

---

## Similar Problems

- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) - Hard
- [Heaters](https://leetcode.com/problems/heaters/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #greedy
  - [[Binary Search]] [[Greedy]] [[Arrays]]
  - **Problem Link:** [LeetCode 1482 - Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
