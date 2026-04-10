---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Upper Bound

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Adobe #Meta #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

## Pattern

Binary Search (Sorted Search Space)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- Find the **smallest index `i`** in a sorted array such that `arr[i] > target`.
- Unlike Lower Bound (which is `arr[i] >= target`), Upper Bound looks for a value **strictly greater** than the target.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- If `arr[mid] > target`, then `mid` is a potential answer; narrow search to the left (`high = mid - 1`).
- Otherwise, the target is still larger or equal; move to the right (`low = mid + 1`).

---

## Approach

### Brute Force
- Linear search through the array from index 0. Return the first index where `arr[i] > x`.
- Time: O(N)

### Optimal
- Use **Binary Search** to divide the search space.
- Maintain an `ans` variable initialized to the array length (default if no element is greater).
- Time: O(log N)

---

## Code (Python)

```python
class Solution:
    def upperBound(self, arr: list[int], n: int, x: int) -> int:
        low = 0
        high = n - 1
        ans = n # Default: target is greater than all elements
        
        while low <= high:
            mid = (low + high) // 2
            
            # If strictly greater, this is a candidate
            if arr[mid] > x:
                ans = mid
                # Look for an even smaller index on the left
                high = mid - 1
            else:
                # Value is <= x, answer must be on the right
                low = mid + 1
                
        return ans
```

---

## Dry Run (Smart Example)

Input: `arr = [1, 2, 4, 4, 5, 6, 8]`, `x = 4`, `n = 7`

| Step | Variables (low, high, mid) | arr[mid] | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | low=0, high=6, mid=3 | 4 | `4 <= 4`, move `low = mid + 1` (low=4). |
| 2 | low=4, high=6, mid=5 | 6 | `6 > 4`, `ans = 5`, move `high = mid - 1` (high=4). |
| 3 | low=4, high=4, mid=4 | 5 | `5 > 4`, `ans = 4`, move `high = mid - 1` (high=3). |
| 4 | low=4, high=3 | - | `low > high`, exit loop. Result: **4**. |

---

## Edge Cases

- **Target > All Elements:** Returns `n` (array size).
- **Target < All Elements:** Returns index `0`.
- **Empty Array:** Returns `0`.
- **All Elements Identical:** If `arr[i] > x`, returns `0`; else returns `n`.

---

## Mistakes

- Using `arr[mid] >= x` instead of `arr[mid] > x` (this computes Lower Bound).
- Forgetting to initialize `ans = n` which leads to errors when target is the largest element.
- Off-by-one errors in `mid` calculation or loop boundaries.
- **User Mistake:** No specific note provided. (Ensure to dry run duplicates manually to grasp the boundary shift).

---

## Complexity

Time: O(log N) → The search space is halved in every iteration.  
Space: O(1) → Only a few pointers (`low`, `high`, `mid`, `ans`) are used.

---

## Similar Problems

- [Lower Bound](https://www.geeksforgeeks.org/problems/implement-lower-bound/1) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #searching
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [GeeksforGeeks - Implement Upper Bound](https://www.geeksforgeeks.org/problems/implement-upper-bound/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
