---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Floor And Celling In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Samsung #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]

## Pattern

Modified Binary Search (Range Bound Search)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The floor of $X$ is the largest element $\le X$. The ceiling of $X$ is the smallest element $\ge X$. In a sorted array, Binary Search naturally converges such that when the loop (`low <= high`) ends without finding $X$, `high` points to the **floor** and `low` points to the **ceiling**.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If target not found: **Floor = arr[high]**, **Ceiling = arr[low]**. Always check if `high < 0` (no floor) or `low >= n` (no ceiling).

---

## Approach

### Brute Force
- Iterate through the array and keep track of the largest element $\le X$ and smallest $\ge X$.
- Time: $O(N)$
- Space: $O(1)$

### Optimal
- Use Binary Search to find the element.
- If `arr[mid] == X`, both floor and ceiling are $X$.
- If `arr[mid] < X`, move `low = mid + 1`.
- If `arr[mid] > X`, move `high = mid - 1`.
- After the loop, validate `high` and `low` indices.

---

## Code (Python)

```python
def find_floor_ceil(arr, x):
    n = len(arr)
    low, high = 0, n - 1
    f, c = -1, -1
    
    while low <= high:
        mid = low + (high - low) // 2
        
        if arr[mid] == x:
            return arr[mid], arr[mid]
        elif arr[mid] < x:
            f = arr[mid] # Potential floor
            low = mid + 1
        else:
            c = arr[mid] # Potential ceiling
            high = mid - 1
            
    return f, c

# Usage
# arr = [1, 2, 8, 10, 10, 12, 19], x = 5
# Output: (2, 8)
```

---

## Dry Run (Smart Example)

**Input:** `arr = [3, 4, 7, 8, 10]`, `x = 5`

| Step | low | high | mid | arr[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 4 | 2 | 7 | $7 > 5$, so Ceiling = 7, `high = 1` |
| 2 | 0 | 1 | 0 | 3 | $3 < 5$, so Floor = 3, `low = 1` |
| 3 | 1 | 1 | 1 | 4 | $4 < 5$, so Floor = 4, `low = 2` |
| 4 | 2 | 1 | - | - | `low > high`, loop ends. Result: (4, 7) |

---

## Edge Cases

- **X is smaller than all:** `floor` will be -1, `ceil` will be `arr[0]`.
- **X is larger than all:** `floor` will be `arr[n-1]`, `ceil` will be -1.
- **X exists in array:** Both `floor` and `ceil` equal $X$.
- **Duplicates:** Binary search handles duplicates correctly for floor/ceil values.
- **Empty Array:** Handled by `low <= high` condition (returns -1, -1).

---

## Mistakes

- **Index Out of Bounds:** Forgetting to check if `high` or `low` went out of range before returning.
- **Off-by-one:** Using `low < high` instead of `low <= high` in the while loop.
- **Initialization:** Initializing `f` and `c` with values present in the array instead of a sentinel like -1.
- **User Mistake:** Ensure revision notes are created for all fundamental BS variations (Lower Bound, Upper Bound, Floor, Ceil).

---

## Complexity

Time: $O(\log N)$ → Binary search cuts the search space in half each iteration.  
Space: $O(1)$ → Constant space used for pointers and variables.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #searching
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [GeeksforGeeks - Floor in Sorted Array](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
