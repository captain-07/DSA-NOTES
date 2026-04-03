---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Lower Bound

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #searching [[Searching]]

## Pattern

Binary Search (Boundary Seeking)  
Sorted Search Space  

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The goal is to find the **smallest index `i`** such that `arr[i] >= x`. In a sorted array, if the middle element satisfies the condition, it is a *potential* candidate, but we must continue searching the left half to find an even smaller index.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `arr[mid] >= target`, store `mid` as the answer and search the left half (`high = mid - 1`). Otherwise, search the right half (`low = mid + 1`). Initialize `ans` to `n` (length of array).

---

## Approach

### Brute Force
- Linear search through the array from index 0 to $n-1$.
- Return the first index where `arr[i] >= target`.
- **Time Complexity:** $O(n)$

### Optimal
- Use **Binary Search** since the array is sorted.
- Initialize `low = 0`, `high = n - 1`, and `ans = n`.
- Calculate `mid`. 
- If `arr[mid] >= target`: `ans = mid`, `high = mid - 1` (Try to find a smaller index).
- Else: `low = mid + 1` (Current value too small).
- **Time Complexity:** $O(\log n)$

---

## Code (Python)

```python
def find_lower_bound(arr, target):
    n = len(arr)
    low = 0
    high = n - 1
    ans = n  # Default if no element is >= target

    while low <= high:
        mid = (low + high) // 2
        
        # If mid element is a potential answer
        if arr[mid] >= target:
            ans = mid
            # Look for a smaller index on the left
            high = mid - 1
        else:
            # Look on the right
            low = mid + 1
            
    return ans
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 4, 5, 6, 7]`, `target = 4`

| Step | Low | High | Mid | `arr[mid]` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 4 | $4 \ge 4$. `ans = 3`, search left (`high = 2`). |
| 2 | 0 | 2 | 1 | 2 | $2 < 4$. `ans` remains 3, search right (`low = 2`). |
| 3 | 2 | 2 | 2 | 4 | $4 \ge 4$. `ans = 2`, search left (`high = 1`). |
| 4 | 2 | 1 | - | - | Loop ends (`low > high`). Result = 2. |

---

## Edge Cases

- **Target > Max Element:** Returns `n` (index out of bounds).
- **Target < Min Element:** Returns `0`.
- **Empty Array:** Returns `0`.
- **All Elements Identical:** Returns `0` if `arr[0] >= target`.
- **Target in Middle (Duplicates):** Returns the *first* occurrence.

---

## Mistakes

- **Incorrect Initialization:** Forgetting to initialize `ans = n`.
- **Early Exit:** Returning `mid` immediately when `arr[mid] == target` (This is standard Binary Search, not Lower Bound).
- **Boundary Error:** Using `high = mid` instead of `high = mid - 1`, causing infinite loops.
- **User Mistake:** No specific note provided (Ensure to document the specific logic for finding the *first* instance).

---

## Complexity

Time: $O(\log n)$ → The search space is halved in every iteration.  
Space: $O(1)$ → Only a few variables are used regardless of input size.

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #searching #lowerbound
  - [[Binary Search]] [[Searching]]
  - **Revision Date:** 2026-04-03

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
