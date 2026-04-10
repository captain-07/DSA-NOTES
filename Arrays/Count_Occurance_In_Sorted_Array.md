---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Count Occurance In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Samsung

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Array]]

## Pattern

Modified Binary Search (Boundary Search)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

In a sorted array, all occurrences of a target value are contiguous. Instead of a linear scan, use **Binary Search** twice to find the leftmost (first) and rightmost (last) indices of the target. The count is simply `(last - first + 1)`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find `first_occurrence` and `last_occurrence` using Binary Search. If `first == -1`, return `0`. Otherwise, return `last - first + 1`.

---

## Approach

### Brute Force
- Linear scan through the array and increment a counter whenever the target is found.
- Time: O(N) | Space: O(1)

### Optimal
- Use two separate binary search functions (or one parameterized function) to find:
    1. The **first** index where `arr[i] == target`.
    2. The **last** index where `arr[i] == target`.
- Logic: When `arr[mid] == target`, don't stop; move the `high` pointer (for first) or `low` pointer (for last) to find the boundary.
- Time: O(log N) | Space: O(1)

---

## Code (Python)

```python
class Solution:
    def countOccurrences(self, arr: list[int], n: int, x: int) -> int:
        first = self.findFirst(arr, n, x)
        if first == -1:
            return 0
        last = self.findLast(arr, n, x)
        return last - first + 1

    def findFirst(self, arr, n, x):
        low, high = 0, n - 1
        res = -1
        while low <= high:
            mid = low + (high - low) // 2
            if arr[mid] == x:
                res = mid
                high = mid - 1 # Keep looking left
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1
        return res

    def findLast(self, arr, n, x):
        low, high = 0, n - 1
        res = -1
        while low <= high:
            mid = low + (high - low) // 2
            if arr[mid] == x:
                res = mid
                low = mid + 1 # Keep looking right
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1
        return res
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 4, 4, 5, 6]`, `x = 4`

| Step | Function | Mid (Val) | Action | Range (Low, High) | res |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `findFirst` | 3 (4) | Target found, search Left | [0, 2] | 3 |
| 2 | `findFirst` | 1 (2) | 2 < 4, search Right | [2, 2] | 3 |
| 3 | `findFirst` | 2 (4) | Target found, search Left | [2, 1] (End) | 2 |
| 4 | `findLast` | 3 (4) | Target found, search Right | [4, 6] | 3 |
| 5 | `findLast` | 5 (5) | 5 > 4, search Left | [4, 4] | 3 |
| 6 | `findLast` | 4 (4) | Target found, search Right | [5, 4] (End) | 4 |

**Result:** `last(4) - first(2) + 1 = 3`

---

## Edge Cases

- **Target not in array:** `findFirst` returns -1, function returns 0.
- **Empty array:** Handled by loop conditions; returns 0.
- **All elements are target:** `first` becomes 0, `last` becomes `n-1`.
- **Single element array:** Binary search handles range correctly.

---

## Mistakes

- Using linear search inside a binary search (e.g., finding the first occurrence then scanning right) results in O(N) worst case (e.g., all elements are the same).
- Forgetting the `first == -1` check before calculating the difference.
- User mistake: None.

---

## Complexity

Time: O(log N) → Two independent binary searches performed.
Space: O(1) → Only a few pointers/variables used.

---

## Similar Problems

- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Find Peak Element](https://leetcode.com/problems/find-peak-element/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #searching
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [GeeksforGeeks - Count occurrences in a sorted array](https://www.geeksforgeeks.org/problems/count-occurences-of-a-number-in-a-sorted-array1249/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
