---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Floor And Celling In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Flipkart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

## Pattern

Binary Search (Boundary Search)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The problem asks for two boundaries: the largest value $\le X$ (Floor) and the smallest value $\ge X$ (Ceiling). Since the array is sorted, we use **Binary Search** to eliminate half the search space. For Floor, we keep track of the last element $\le X$ while moving right; for Ceiling, we track the last element $\ge X$ while moving left.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Ceiling** is identical to `Lower Bound` (first element $\ge X$).
- **Floor** is the element at `high` after a standard binary search if $X$ is not found.
- If $X$ exists in the array, both Floor and Ceiling are $X$.

---

## Approach

### Brute Force
- Linear scan through the array to find the two boundaries.
- Time: $O(N)$
- Space: $O(1)$

### Optimal
- Use two separate Binary Search passes or one modified pass.
- For **Floor**: If `arr[mid] <= x`, it's a candidate; search right (`low = mid + 1`).
- For **Ceiling**: If `arr[mid] >= x`, it's a candidate; search left (`high = mid - 1`).
- Time: $O(\log N)$
- Space: $O(1)$

---

## Code (Python)

```python
class Solution:
    def getFloorAndCeil(self, arr: list[int], n: int, x: int) -> tuple[int, int]:
        """
        Returns (floor, ceiling) of x in sorted array arr.
        -1 if not found.
        """
        # Calculate Floor
        f_ans = -1
        low, high = 0, n - 1
        while low <= high:
            mid = low + (high - low) // 2
            if arr[mid] <= x:
                f_ans = arr[mid]
                low = mid + 1
            else:
                high = mid - 1
                
        # Calculate Ceiling (Lower Bound)
        c_ans = -1
        low, high = 0, n - 1
        while low <= high:
            mid = low + (high - low) // 2
            if arr[mid] >= x:
                c_ans = arr[mid]
                high = mid - 1
            else:
                low = mid + 1
                
        return (f_ans, c_ans)
```

---

## Dry Run (Smart Example)

**Input:** `arr = [3, 4, 7, 8, 8, 10]`, `x = 5`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `low=0, high=5, mid=2 (arr[2]=7)` | `7 > 5`: Ceiling candidate = 7, search left for Ceil. |
| 2 | `low=0, high=1, mid=0 (arr[0]=3)` | `3 < 5`: Floor candidate = 3, search right for Floor. |
| 3 | `low=1, high=1, mid=1 (arr[1]=4)` | `4 < 5`: Floor candidate = 4, search right. |
| 4 | `low=2, high=1` | Loop terminates. **Floor: 4, Ceil: 7**. |

---

## Edge Cases

- **X smaller than min element:** Floor is -1, Ceiling is `arr[0]`.
- **X larger than max element:** Floor is `arr[n-1]`, Ceiling is -1.
- **X exists in array:** Both Floor and Ceiling are $X$.
- **Empty Array:** Handled by `low <= high` (returns -1, -1).
- **Duplicate elements:** Binary search correctly identifies the nearest boundary.

---

## Mistakes

- Confusing Floor with Ceiling logic (remember: Floor is "down", Ceiling is "up").
- Forgetting to handle the case where $X$ is out of array bounds.
- **Critical:** Not mastering fundamental BS variations (Lower Bound, Upper Bound, Floor, Ceil) which are the building blocks for harder problems.

---

## Complexity

Time: $O(\log N)$ → We perform two binary searches, each halving the search space.  
Space: $O(1)$ → No extra space used besides a few variables.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch
  - [[Binary Search]] [[Lower Bound]] [[Searching]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [GeeksforGeeks - Floor and Ceil](https://www.geeksforgeeks.org/problems/ceil-the-floor0532/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
