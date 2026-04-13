---
created: 2026-04-13
revisions:
  - 2026-04-15
  - 2026-04-20
  - 2026-04-28
  - 2026-05-13
---

# Kth Missing Number

---

## Pattern

Binary Search on Index (Missing Count)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

In a sorted array, for any index `i`, the number of missing elements before `arr[i]` is exactly:  
**`missing = arr[i] - (i + 1)`**  
We use Binary Search to find the first index where the number of missing elements is $\ge k$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the boundary where `arr[mid] - (mid + 1) < k`. The answer is simply `k + low` (where `low` is the insertion point).

---

## Approach

### Brute Force
Iterate from $1$ to $\infty$. If a number is not in `arr`, decrement $k$. When $k=0$, return that number.  
**Time:** $O(N + K)$

### Better
Iterate through the array. If `arr[i] <= k`, it means one "missing slot" before $k$ is actually filled, so increment $k$ to shift the window.  
**Time:** $O(N)$

### Optimal
Perform Binary Search to find the largest index `high` where `missing < k`.
1. `low, high = 0, len(arr) - 1`
2. While `low <= high`:
   - `mid = (low + high) // 2`
   - `missing = arr[mid] - (mid + 1)`
   - If `missing < k`: `low = mid + 1`
   - Else: `high = mid - 1`
3. The $k$-th missing number is `low + k`.

---

## Code (Python)

```python
class Solution:
    def findKthPositive(self, arr: list[int], k: int) -> int:
        low = 0
        high = len(arr) - 1
        
        while low <= high:
            mid = (low + high) // 2
            # Calculate how many numbers are missing at index mid
            missing = arr[mid] - (mid + 1)
            
            if missing < k:
                low = mid + 1
            else:
                high = mid - 1
        
        # Result = arr[high] + (k - missing_at_high)
        # Simplified: low + k
        return low + k
```

---

## Dry Run (Smart Example)

**Input:** `arr = [2, 3, 4, 7, 11]`, `k = 5`

| Step | low | high | mid | arr[mid] | Missing (`arr[m]-(m+1)`) | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 4 | 2 | 4 | $4 - (2+1) = 1$ | $1 < 5 \to$ low = 3 |
| 2 | 3 | 4 | 3 | 7 | $7 - (3+1) = 3$ | $3 < 5 \to$ low = 4 |
| 3 | 4 | 4 | 4 | 11 | $11 - (4+1) = 6$ | $6 \ge 5 \to$ high = 3 |
| **End** | **4** | 3 | - | - | - | **Return low + k = 4 + 5 = 9** |

---

## Edge Cases

- **k < arr[0]:** Result is just `k`.
- **k > missing at last index:** Result is `len(arr) + k`.
- **Empty array:** Result is `k`.
- **Sequential array [1, 2, 3]:** Binary search correctly points to the end.

---

## Mistakes

- **Formula Confusion:** Forgetting that `i` is 0-indexed, so the "expected" value is `i + 1`.
- **Result Logic:** Trying to return `arr[high]` directly without accounting for the remaining `k`.
- **User Mistake:** Failing to understand that the sorted property allows us to calculate the "gap count" at any index in $O(1)$, which is the prerequisite for Binary Search.

---

## Complexity

Time: O(log N) → Standard binary search on array indices.  
Space: O(1) → Only constant extra variables used.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Kth Missing Element in Sorted Array](https://leetcode.com/problems/kth-missing-element-in-sorted-array/) - Medium (Premium)
- [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch 
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-13
  - **Problem Link:** [LeetCode - Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Facebook #Google #Microsoft #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-15)
- [ ] Day 7 Revision (2026-04-20)
- [ ] Day 15 Revision (2026-04-28)
- [ ] Day 30 Revision (2026-05-13)
