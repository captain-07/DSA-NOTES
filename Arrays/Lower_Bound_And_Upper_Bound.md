---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Lower Bound And Upper Bound

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #GoldmanSachs #Walmart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

## Pattern

Binary Search on Sorted Search Space

---

## Difficulty

Easy / Medium (Foundational for advanced BS problems)  
#easy

---

## ⚡ Key Idea (Core Insight)

The goal is to find the **first index** that satisfies a condition in a sorted array. 
- **Lower Bound:** Smallest index `i` such that `arr[i] >= x`.
- **Upper Bound:** Smallest index `i` such that `arr[i] > x`.
- Instead of returning immediately when `arr[mid] == x`, we "shrink" the search space to find the leftmost possible candidate.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Lower Bound:** `arr[mid] >= target` $\rightarrow$ `ans = mid`, `high = mid - 1`.
- **Upper Bound:** `arr[mid] > target` $\rightarrow$ `ans = mid`, `high = mid - 1`.
- If no such element exists, the answer is the array length `n`.

---

## Approach

### Brute Force
- Linear search through the array from index 0 to $n-1$.
- Return the first index that satisfies the condition ($\ge x$ or $> x$).
- **Time:** $O(N)$

### Optimal
- Use **Binary Search** since the array is sorted.
- Maintain an `ans` variable initialized to `n`.
- Adjust `low` and `high` pointers based on the comparison at `mid`.
- **Time:** $O(\log N)$

---

## Code (Python)

```python
def get_lower_bound(arr, n, x):
    low, high = 0, n - 1
    ans = n # Default if no element >= x
    
    while low <= high:
        mid = (low + high) // 2
        # For Lower Bound: Look for first element >= x
        if arr[mid] >= x:
            ans = mid
            high = mid - 1 # Look for smaller index on the left
        else:
            low = mid + 1
    return ans

def get_upper_bound(arr, n, x):
    low, high = 0, n - 1
    ans = n # Default if no element > x
    
    while low <= high:
        mid = (low + high) // 2
        # For Upper Bound: Look for first element > x
        if arr[mid] > x:
            ans = mid
            high = mid - 1 # Look for smaller index on the left
        else:
            low = mid + 1
    return ans
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 4, 5, 6]`, `target = 4`, `n = 6`

| Step | Type | Low | High | Mid | `arr[mid]` | Action | `ans` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | **LB** | 0 | 5 | 2 | 4 | `4 >= 4`: true, high = 1 | 2 |
| 2 | **LB** | 0 | 1 | 0 | 1 | `1 >= 4`: false, low = 1 | 2 |
| 3 | **LB** | 1 | 1 | 1 | 2 | `2 >= 4`: false, low = 2 | 2 (Loop Ends) |
| 1 | **UB** | 0 | 5 | 2 | 4 | `4 > 4`: false, low = 3 | 6 |
| 2 | **UB** | 3 | 5 | 4 | 5 | `5 > 4`: true, high = 3 | 4 |
| 3 | **UB** | 3 | 3 | 3 | 4 | `4 > 4`: false, low = 4 | 4 (Loop Ends) |

---

## Edge Cases

- **Target > Max element:** Both return `n`.
- **Target < Min element:** Both return `0`.
- **Empty Array:** Returns 0 (if `ans` initialized to `n`).
- **All elements identical:** LB returns 0, UB returns `n`.

---

## Mistakes

- **Incorrect condition:** Using `arr[mid] > x` for Lower Bound (should be `>=`).
- **Binary Search logic:** Forgetting to update the `ans` variable and just returning `low`.
- **Range error:** Returning `n-1` instead of `n` when target is larger than all elements.
- **Infinite Loop:** Not moving `low` or `high` correctly inside the while loop.

---

## Complexity

- **Time:** $O(\log N)$ → Each step halves the search space.
- **Space:** $O(1)$ → Only iterative pointers used.

---

## Tags and Properties

- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Lower Bound]] [[Upper Bound]]
- Revision Date: 2026-04-03
- Related: [[Search Insert Position]], [[First and Last Occurrence]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
