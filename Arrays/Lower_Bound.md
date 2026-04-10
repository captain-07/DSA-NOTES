---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Lower Bound

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

---
## Pattern

Binary Search (Range Reduction)

---
## Difficulty

Easy
#easy

---
## ⚡ Key Idea (Core Insight)

The goal is to find the **smallest index** `i` such that `arr[i] >= x`. In a sorted array, if `arr[mid]` is at least `x`, it *could* be the answer, but a smaller index might also satisfy it, so we search the left half.

---
## ⚡ Quick Recall (VERY IMPORTANT)

If `arr[mid] >= target`, update `ans = mid` and search left (`high = mid - 1`). Otherwise, search right (`low = mid + 1`).

---
## Approach

### Brute Force
- Linear search from index 0 to $n-1$. Return the first index where `arr[i] >= target`.
- **Time Complexity:** O(N)

### Better
- N/A (Binary search is the standard improvement over linear search for sorted data).

### Optimal
1. Initialize `low = 0`, `high = n - 1`, and `ans = n` (default if no element is $\ge$ target).
2. While `low <= high`:
    - Calculate `mid = low + (high - low) // 2`.
    - If `arr[mid] >= target`: Store `ans = mid`, move `high = mid - 1` to find a smaller index.
    - Else: Move `low = mid + 1`.
3. Return `ans`.

---
## Code (Python)

```python
class Solution:
    def lowerBound(self, arr: list[int], n: int, x: int) -> int:
        low = 0
        high = n - 1
        ans = n  # Default to n if no element satisfies the condition
        
        while low <= high:
            mid = low + (high - low) // 2
            
            # If current element is potential lower bound
            if arr[mid] >= x:
                ans = mid
                # Look for a smaller index on the left
                high = mid - 1
            else:
                # Look for larger elements on the right
                low = mid + 1
                
        return ans
```

---
## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 4, 4, 6, 7]`, `x = 4`, `n = 7`

| Step | low, high, mid | arr[mid] | Action | ans |
| :--- | :--- | :--- | :--- | :--- |
| 1 | L:0, H:6, M:3 | 4 | 4 >= 4 (True), H = M-1 | 3 |
| 2 | L:0, H:2, M:1 | 2 | 2 >= 4 (False), L = M+1 | 3 |
| 3 | L:2, H:2, M:2 | 4 | 4 >= 4 (True), H = M-1 | 2 |
| 4 | L:2, H:1 | - | Loop terminates (L > H) | 2 |

**Final Output:** 2

---
## Edge Cases

- **Target smaller than all elements:** Returns index 0.
- **Target larger than all elements:** Returns index `n`.
- **Array with duplicates:** Correcty returns the *first* occurrence.
- **Empty array:** Should be handled by initial bounds (returns 0 or `n`).

---
## Mistakes

- Using `low < high` instead of `low <= high`.
- Returning `mid` immediately when `arr[mid] == x` (Lower bound is the first index $\ge x$, not just equality).
- Forgetting to initialize `ans` to `n`.
- **User Mistake:** No specific note provided.

---
## Complexity

Time: O(log N) → The search space is halved in every iteration.  
Space: O(1) → Only a few variables used for pointers.

---
## Similar Problems

- [Upper Bound](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-in-c/) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium

---
## Tags and Properties

- #dsa #important #revisit #binarysearch #searching
- [[Binary Search]] [[Arrays]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [Search Insert Position (LeetCode)](https://leetcode.com/problems/search-insert-position/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
