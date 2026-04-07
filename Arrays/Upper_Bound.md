---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Upper Bound

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Adobe #MorganStanley

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #searching [[Searching]]

## Pattern

Binary Search (Sorted Array)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The **Upper Bound** of $X$ is the first index $i$ where $arr[i] > X$. In a sorted array, this represents the smallest value strictly greater than the target. If no such element exists, return $N$ (the array size).

---

## ⚡ Quick Recall (VERY IMPORTANT)

If $arr[mid] > X$, then $mid$ is a potential answer; save it and search the **left** half to find a smaller index. Otherwise, search the **right** half.

---

## Approach

### Brute Force
- Linear search from index 0 to $N-1$ and return the first index where $arr[i] > X$.
- Time: O(N)
- Space: O(1)

### Optimal
- Use two pointers (`low`, `high`) for Binary Search.
- Maintain an `ans` variable initialized to $N$.
- Narrow the search space based on whether the current middle element is strictly greater than $X$.
- Time: O(log N)
- Space: O(1)

---

## Code (Python)

```python
def get_upper_bound(arr, n, x):
    low = 0
    high = n - 1
    ans = n # Default if no element > x

    while low <= high:
        mid = (low + high) // 2
        
        # If mid element is strictly greater than x
        if arr[mid] > x:
            ans = mid      # Potential answer
            high = mid - 1 # Try to find a smaller index on the left
        else:
            low = mid + 1  # Search the right half
            
    return ans

# Example usage:
# arr = [1, 2, 4, 4, 5, 6, 8], x = 4
# Output: 4 (index of first element > 4, which is 5)
```

---

## Dry Run (Smart Example)

Input: `arr = [1, 2, 4, 4, 5, 6, 8]`, `n = 7`, `x = 4`

| Step | low, high, mid | arr[mid] | Explanation | ans |
| :--- | :--- | :--- | :--- | :--- |
| 1 | L=0, H=6, M=3 | 4 | 4 is not > 4. Move right: `low = mid + 1`. | 7 |
| 2 | L=4, H=6, M=5 | 6 | 6 > 4. Potential answer. Move left: `high = mid - 1`. | 5 |
| 3 | L=4, H=4, M=4 | 5 | 5 > 4. Potential answer. Move left: `high = mid - 1`. | 4 |
| 4 | L=4, H=3 | - | `low > high`. Loop terminates. | 4 |

**Result: Index 4**

---

## Edge Cases

- **X is greater than all elements:** Loop completes with `ans` remaining $N$.
- **X is smaller than all elements:** Returns index 0.
- **Empty Array:** Should return 0 or handle as per requirement.
- **Array with all same elements (e.g., [4, 4, 4], X=4):** Returns $N$ (3).
- **Array with all same elements (e.g., [5, 5, 5], X=4):** Returns 0.

---

## Mistakes

- Using `arr[mid] >= x` instead of `arr[mid] > x` (that would be Lower Bound).
- Not initializing `ans` to $N$, leading to errors when no element is greater than $X$.
- Returning `mid` immediately when `arr[mid] > x` without searching for a smaller index.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → The search space is halved in every iteration of the binary search.  
Space: O(1) → Only a few variables are used regardless of input size.

---

## Similar Problems

- [Lower Bound](https://www.geeksforgeeks.org/problems/implement-lower-bound/1) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #arrays #searching #stl
  - [[Binary Search]] [[Searching]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [Implement Upper Bound - GFG](https://www.geeksforgeeks.org/problems/implement-upper-bound/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
