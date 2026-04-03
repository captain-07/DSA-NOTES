---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Upper Bound

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #searching [[Searching]]

---
## Pattern

Binary Search (Searching for a boundary condition)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The Upper Bound is the **smallest index `i`** such that `arr[i] > x` (strictly greater). If all elements are less than or equal to `x`, the answer is the length of the array (`n`).

---

## ⚡ Quick Recall (VERY IMPORTANT)

When `arr[mid] > target`, it **could** be the answer, so store `mid` and look left (`high = mid - 1`) to find a smaller index.

---

## Approach

### Brute Force
- Iterate through the array from left to right and return the first index where `arr[i] > target`.
- **Time Complexity:** O(N)

### Optimal
- Use **Binary Search** because the array is sorted.
- Initialize `ans = n`.
- If `arr[mid] > target`: update `ans = mid` and move `high = mid - 1`.
- Else: move `low = mid + 1`.
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
def get_upper_bound(arr, target):
    n = len(arr)
    low = 0
    high = n - 1
    ans = n  # Default if no element is strictly greater
    
    while low <= high:
        mid = (low + high) // 2
        
        # Check if mid element is strictly greater than target
        if arr[mid] > target:
            ans = mid         # Current mid is a candidate
            high = mid - 1    # Look for a smaller index on the left
        else:
            low = mid + 1     # Look on the right
            
    return ans
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 4, 4, 6, 7]`, `target = 4`

| Step | Low | High | Mid | arr[mid] | Condition (arr[mid] > 4) | Action | ans |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 4 | False (4 > 4 is False) | low = 4 | 7 |
| 2 | 4 | 6 | 5 | 6 | True (6 > 4 is True) | ans = 5, high = 4 | 5 |
| 3 | 4 | 4 | 4 | 4 | False (4 > 4 is False) | low = 5 | 5 |
| 4 | 5 | 4 | - | - | Loop Breaks (low > high) | Return ans | 5 |

**Result:** Index 5 (Value 6)

---

## Edge Cases

- **Target > Max element:** Returns `n` (length of array).
- **Target < Min element:** Returns `0`.
- **Empty Array:** Returns `0` (initial `ans = n`).
- **All elements identical to target:** Returns `n`.
- **Array with duplicates:** Correcty skips all duplicates to find the first strictly greater element.

---

## Mistakes

- **Confusing with Lower Bound:** Lower bound is `arr[i] >= target`; Upper bound is `arr[i] > target`.
- **Returning `mid` immediately:** You must keep searching left even after finding a match to ensure it's the *first* such index.
- **Off-by-one error:** Initializing `high` or `ans` incorrectly.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Range is halved in every iteration of binary search.  
Space: O(1) → Only a few variables used; no extra space relative to input size.

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #searching #sorting
  - [[Binary Search]] [[Arrays]]
  - Revision Date: 2026-04-03

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
