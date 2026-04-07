---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Lower Bound

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Adobe #Flipkart

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern

Binary Search (Boundary Search)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

The goal is to find the **smallest index** `i` such that `arr[i] >= x`. Unlike standard binary search, finding the element is not enough; we must continue searching the left half to ensure it is the *first* such instance.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `arr[mid] >= target`, it's a potential answer. Record `mid` and move **left** (`high = mid - 1`) to find a smaller index.

---

## Approach

### Brute Force
- Iterate from index `0` to `n-1`. Return the first index where `arr[i] >= target`.
- **Time Complexity:** O(N)

### Optimal
- Use Binary Search. Maintain a variable `ans` initialized to `n` (size of array).
- If `arr[mid] >= target`, update `ans = mid` and search left (`high = mid - 1`).
- Otherwise, search right (`low = mid + 1`).
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
def lower_bound(arr, target):
    n = len(arr)
    low = 0
    high = n - 1
    ans = n # Default if no element >= target

    while low <= high:
        mid = (low + high) // 2
        
        # If mid element is a candidate for lower bound
        if arr[mid] >= target:
            ans = mid
            # Try to find a smaller index on the left
            high = mid - 1
        else:
            # Target is larger, search right half
            low = mid + 1
            
    return ans
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 4, 4, 6, 7]`, `target = 4`

| Step | low | high | mid | arr[mid] | Action | ans |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 4 | `4 >= 4`, record index 3, move left | 3 |
| 2 | 0 | 2 | 1 | 2 | `2 < 4`, move right | 3 |
| 3 | 2 | 2 | 2 | 4 | `4 >= 4`, record index 2, move left | 2 |
| 4 | 2 | 1 | - | - | `low > high`, Break | 2 |

**Result:** 2 (Index of the first '4')

---

## Edge Cases

- **Target > Max Element:** Returns `n` (insertion point at the end).
- **Target < Min Element:** Returns `0`.
- **Array with Duplicates:** Correct identifies the first occurrence.
- **Empty Array:** Returns `0`.

---

## Mistakes

- **Stopping at first match:** Standard binary search returns as soon as `arr[mid] == target`. Lower bound must keep looking left.
- **Incorrect Initialization:** `ans` should be initialized to `len(arr)`, not `-1`, as the lower bound can be the end of the array.
- **Logic for Finding First Instance:** Ensure `high = mid - 1` is called even when `arr[mid] == target`.

---

## Complexity

Time: O(log N) → Range is halved in each iteration.  
Space: O(1) → Only a few pointers used.

---

## Similar Problems

- [Upper Bound](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-in-c/) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First and Last Position of Element](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #searching #first-occurrence
  - [[Binary Search]] [[Searching Algorithms]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Search Insert Position](https://leetcode.com/problems/search-insert-position/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
