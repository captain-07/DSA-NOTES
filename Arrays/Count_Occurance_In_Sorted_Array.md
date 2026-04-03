---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Count Occurance In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #TCS #Samsung

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Array]]

## Pattern

Modified Binary Search (First and Last Occurrence)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

In a **sorted** array, all occurrences of a target element are contiguous. The total count is simply:  
`(index_of_last_occurrence - index_of_first_occurrence) + 1`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Perform two Binary Searches: one to find the **leftmost** index and one for the **rightmost** index. If the first index is `-1`, the count is `0`.

---

## Approach

### Brute Force
- Traverse the entire array linearly and increment a counter whenever the target is found.
- **Time Complexity:** O(N)

### Optimal
- **Step 1:** Use Binary Search to find the first occurrence. If `arr[mid] == target`, instead of returning, search the left half (`high = mid - 1`) to find a potential earlier occurrence.
- **Step 2:** Use Binary Search to find the last occurrence. If `arr[mid] == target`, search the right half (`low = mid + 1`).
- **Step 3:** Result = `(last - first + 1)`.
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
def count_occurrences(arr, n, x):
    def find_bound(is_first):
        low, high = 0, n - 1
        res = -1
        while low <= high:
            mid = (low + high) // 2
            if arr[mid] == x:
                res = mid
                if is_first:
                    high = mid - 1  # Look for earlier occurrence
                else:
                    low = mid + 1   # Look for later occurrence
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1
        return res

    first = find_bound(True)
    if first == -1: return 0
    last = find_bound(False)
    
    return last - first + 1

# Example usage:
# arr = [1, 2, 2, 2, 2, 3], x = 2 -> Output: 4
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 4, 4, 5, 6]`, `target = 4`

| Step | Search Type | Low | High | Mid | `arr[mid]` | Result/Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Find First | 0 | 6 | 3 | 4 | Found! `res=3`, `high=2` |
| 2 | Find First | 0 | 2 | 1 | 2 | `low=2` |
| 3 | Find First | 2 | 2 | 2 | 4 | Found! `res=2`, `high=1` (Loop ends) |
| 4 | Find Last | 0 | 6 | 3 | 4 | Found! `res=3`, `low=4` |
| 5 | Find Last | 4 | 6 | 5 | 5 | `high=4` |
| 6 | Find Last | 4 | 4 | 4 | 4 | Found! `res=4`, `low=5` (Loop ends) |

**Final Count:** `4 - 2 + 1 = 3`

---

## Edge Cases

- **Target not in array:** `first` returns -1, function returns 0.
- **Empty array:** Loop never starts, returns 0.
- **All elements are target:** `first=0`, `last=n-1`, count is `n`.
- **Target at boundaries:** Handled correctly by standard Binary Search logic.

---

## Mistakes

- Using O(N) linear search on a sorted array (loses interview points).
- Forgetting the `+ 1` in `last - first + 1`.
- Not handling the case where the target isn't found (check for `-1`).
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Two binary searches take 2 * O(log N), which simplifies to O(log N).  
Space: O(1) → Iterative binary search uses constant extra space.

---

## Tags and Properties

- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Arrays]]
- Revision Date: 2026-04-03
- Related Problems: [[Find First and Last Position of Element in Sorted Array]], [[Search in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
