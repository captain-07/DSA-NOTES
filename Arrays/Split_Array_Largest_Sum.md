---
created: 2026-04-18
revisions:
  - 2026-04-20
  - 2026-04-25
  - 2026-05-03
  - 2026-05-18
---

# Split Array Largest Sum

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Meta #ByteDance #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #greedy [[Greedy]]
  - #dynamicprogramming [[Dynamic Programming]]

## Pattern

Binary Search on Answer (Minimizing the Maximum)

---
## Difficulty

Hard  
#hard

---

## ⚡ Key Idea (Core Insight)

The answer must fall between `max(nums)` (each element in its own subarray) and `sum(nums)` (all elements in one subarray). Since the "possibility" of splitting the array follows a monotonic property (if we can split with a max sum of $X$, we can also do it with $X+1$), we **Binary Search for the smallest valid sum**.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Range is `[max(array), sum(array)]`. For each `mid`, use a **Greedy** pass to count required subarrays. If `count > k`, `mid` is too small.

---

## Approach

### Brute Force
- Use recursion to try every possible split point to partition the array into $k$ segments.
- **Time Complexity:** $O(N^C_{k-1})$ — Exponential.

### Better
- Dynamic Programming: `dp[i][j]` is the min-max sum splitting first `i` elements into `j` subarrays.
- **Time Complexity:** $O(N^2 \cdot K)$.

### Optimal
1. Define search space: `low = max(nums)`, `high = sum(nums)`.
2. While `low <= high`:
   - Pick `mid`.
   - Check `canSplit(mid)`: Iterate greedily, starting a new subarray whenever the current sum exceeds `mid`.
   - If `subarrays_needed <= k`: This `mid` works; try smaller (`high = mid - 1`).
   - Else: `mid` is too small; try larger (`low = mid + 1`).
3. Return `low`.

---

## Code (Python)

```python
class Solution:
    def splitArray(self, nums: list[int], k: int) -> int:
        # Range of the answer
        low, high = max(nums), sum(nums)
        ans = high
        
        def can_split(max_sum: int) -> bool:
            subarrays = 1
            current_sum = 0
            for num in nums:
                if current_sum + num > max_sum:
                    subarrays += 1
                    current_sum = num
                else:
                    current_sum += num
            return subarrays <= k

        while low <= high:
            mid = (low + high) // 2
            # If possible to split with max sum 'mid', try smaller
            if can_split(mid):
                ans = mid
                high = mid - 1
            else:
                # mid is too small, must increase sum capacity
                low = mid + 1
        
        return ans # or return low
```

---

## Dry Run (Smart Example)

**Input:** `nums = [7,2,5,10,8], k = 2`  
**Initial Range:** `low = 10`, `high = 32`

| Step | mid | `can_split(mid)` | Subarrays Found | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 21 | True | `[7,2,5], [10,8]` (2) | `high = 20`, `ans = 21` |
| 2 | 15 | False | `[7,2,5], [10], [8]` (3) | `low = 16` |
| 3 | 18 | True | `[7,2,5], [10,8]` (2) | `high = 17`, `ans = 18` |
| 4 | 16 | False | `[7,2,5], [10], [8]` (3) | `low = 17` |
| 5 | 17 | False | `[7,2,5], [10], [8]` (3) | `low = 18` |

**Final Result:** `low = 18`

---

## Edge Cases

- **k = 1:** Answer is `sum(nums)`.
- **k = len(nums):** Answer is `max(nums)`.
- **Large elements:** Python handles large integers, but ensure no overflow in other languages.
- **Array with identical elements:** Binary search handles this naturally.

---

## Mistakes

- **Incorrect `low`:** Starting `low` at 0 or 1 instead of `max(nums)`. A subarray sum cannot be smaller than the largest element.
- **Comparison Confusion:** In `can_split`, remember: `current_sum + num > mid` means the current number **must** start a new subarray.
- **Opposite Polarity (The `low` vs `high` return):**
  - When the loop `low <= high` ends, `high` is at the last "False" (impossible) value, and `low` is at the first "True" (possible) value. 
  - Since we want the **minimum** value that makes `can_split` True, we return `low`.
  - Think of it as: `high` collapses from the right (possible side), and `low` pushes from the left (impossible side). They cross exactly at the boundary.

---

## Complexity

Time: O(N * log(Sum - Max)) → N is array length; log term is the binary search range.  
Space: O(1) → Only variables used for range and greedy check.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) - Medium
- [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/) - Medium
- [Aggressive Cows](https://www.spoj.com/problems/AGGRCOW/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #minimax #greedy
  - [[Binary Search]] [[Greedy]] [[Array]]
  - Revision Date: 2026-04-18
  - **Problem Link:** [LeetCode - Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-20)
- [ ] Day 7 Revision (2026-04-25)
- [ ] Day 15 Revision (2026-05-03)
- [ ] Day 30 Revision (2026-05-18)
