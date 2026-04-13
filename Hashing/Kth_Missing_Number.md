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

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Facebook #Google #Microsoft #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Array]]

## Pattern

Binary Search on Range/Value + Index-to-Value Mapping

---
## Difficulty

Easy / Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

In a sorted array `arr`, the number of missing integers before index `i` is exactly **`arr[i] - (i + 1)`**. 
We use Binary Search to find the largest index where the number of missing elements is still less than `k`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the first index `low` where `arr[low] - (low + 1) >= k`. The answer is always **`low + k`**.

---

## Approach

### Brute Force
Iterate from 1 upwards. If the number is in `arr`, skip it; if not, decrement `k`. When `k == 0`, return the number.
- **Time:** $O(N + K)$
- **Space:** $O(1)$

### Better (Linear Scan)
Iterate through `arr`. If `arr[i] <= k`, it means one "missing slot" before `k` is actually filled, so increment `k`.
- **Time:** $O(N)$

### Optimal (Binary Search)
1. Initialize `low = 0`, `high = len(arr) - 1`.
2. While `low <= high`:
   - Calculate `mid`.
   - `missing = arr[mid] - (mid + 1)`.
   - If `missing < k`, move `low = mid + 1`.
   - Else, move `high = mid - 1`.
3. The answer is `low + k`. (Logic: After the loop, `high` is the largest index where missing < `k`. Result is `arr[high] + (k - missing_at_high)`, which simplifies to `low + k`).

---

## Code (Python)

```python
class Solution:
    def findKthPositive(self, arr: list[int], k: int) -> int:
        low = 0
        high = len(arr) - 1
        
        while low <= high:
            mid = (low + high) // 2
            # Elements missing before index mid
            missing = arr[mid] - (mid + 1)
            
            if missing < k:
                low = mid + 1
            else:
                high = mid - 1
                
        # Final formula: low + k
        return low + k
```

---

## Dry Run (Smart Example)

**Input:** `arr = [2, 3, 4, 7, 11]`, `k = 5`

| Step | low | high | mid | arr[mid] | Missing: `arr[mid]-(mid+1)` | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 4 | 2 | 4 | $4 - (2+1) = 1$ | $1 < 5 \rightarrow$ `low = 3` |
| 2 | 3 | 4 | 3 | 7 | $7 - (3+1) = 3$ | $3 < 5 \rightarrow$ `low = 4` |
| 3 | 4 | 4 | 4 | 11 | $11 - (4+1) = 6$ | $6 \geq 5 \rightarrow$ `high = 3` |
| End | **4** | 3 | - | - | - | Return `low + k = 4 + 5 = 9` |

---

## Edge Cases

- **k is smaller than arr[0]:** Result is just `k`.
- **k is larger than all missing in arr:** Result is `arr[-1] + (k - missing_at_end)`.
- **Array has no missing numbers (e.g., [1, 2, 3]):** Result is `len(arr) + k`.
- **Single element array:** Binary search still handles correctly.

---

## Mistakes

- **Formula Confusion:** Forgetting that `missing = arr[mid] - (mid + 1)`.
- **Optimal Intuition:** Failing to see that the gap between value and index represents the missing count.
- **Result Return:** Returning `low` or `high` instead of the derived value `low + k`.
- **User Mistake:** "dont understand optimal approach" — The key is recognizing that sorted property + index math allows $O(\log N)$ instead of $O(N)$.

---

## Complexity

Time: $O(\log N)$ → Binary search halves the search space each step.  
Space: $O(1)$ → No extra data structures used.

---

## Similar Problems

- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) - Medium
- [Missing Number](https://leetcode.com/problems/missing-number/) - Easy
- [Kth Missing Element in Sorted Array](https://leetcode.com/problems/kth-missing-element-in-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch 
  - [[Binary Search]] [[Array]]
  - Revision Date: 2026-04-13
  - **Problem Link:** [LeetCode 1539 - Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-15)
- [ ] Day 7 Revision (2026-04-20)
- [ ] Day 15 Revision (2026-04-28)
- [ ] Day 30 Revision (2026-05-13)
