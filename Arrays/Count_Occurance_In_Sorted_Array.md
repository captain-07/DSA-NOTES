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
  - #Amazon #Microsoft #Adobe #Zoho #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Arrays]]

## Pattern

Binary Search (Boundary Finding)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Since the array is **sorted**, all occurrences of a target `x` are contiguous. Instead of a linear scan, use **Binary Search** twice to find the `first_occurrence` and `last_occurrence` of `x`. The count is simply `(last - first + 1)`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

`Count = LastIndex - FirstIndex + 1`. Use modified Binary Search to find boundaries in $O(\log N)$.

---

## Approach

### Brute Force
- Linearly traverse the array and increment a counter whenever the target is found.
- **Time Complexity:** $O(N)$

### Optimal
1. **Find First Occurrence:** Run Binary Search. If `arr[mid] == x`, record index and move `high = mid - 1` to search left.
2. **Find Last Occurrence:** Run Binary Search. If `arr[mid] == x`, record index and move `low = mid + 1` to search right.
3. **Result:** If the target isn't found, return 0. Otherwise, return `last - first + 1`.

---

## Code (Python)

```python
class Solution:
    def countOccurrences(self, arr: list[int], x: int) -> int:
        n = len(arr)
        
        def find_bound(is_first: bool) -> int:
            low, high = 0, n - 1
            res = -1
            while low <= high:
                mid = (low + high) // 2
                if arr[mid] == x:
                    res = mid
                    if is_first:
                        high = mid - 1 # Look left
                    else:
                        low = mid + 1  # Look right
                elif arr[mid] < x:
                    low = mid + 1
                else:
                    high = mid - 1
            return res

        first = find_bound(True)
        if first == -1:
            return 0
            
        last = find_bound(False)
        return last - first + 1
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 2, 2, 3]`, `x = 2`

| Step | Operation | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Find First | `low=0, high=4, mid=2` | `arr[2]==2`. `res=2`, `high=1`. |
| 2 | Find First | `low=0, high=1, mid=0` | `arr[0]==1 < 2`. `low=1`. |
| 3 | Find First | `low=1, high=1, mid=1` | `arr[1]==2`. `res=1`, `high=0`. Loop Ends. |
| 4 | Find Last | `low=0, high=4, mid=2` | `arr[2]==2`. `res=2`, `low=3`. |
| 5 | Find Last | `low=3, high=4, mid=3` | `arr[3]==2`. `res=3`, `low=4`. |
| 6 | Find Last | `low=4, high=4, mid=4` | `arr[4]==3 > 2`. `high=3`. Loop Ends. |
| **End** | Result | `3 - 1 + 1 = 3` | Correct count. |

---

## Edge Cases

- **Target not in array:** Binary search returns -1; result should be 0.
- **Empty array:** Handle gracefully (returns 0).
- **All elements are target:** `first = 0`, `last = n-1`.
- **Target at boundaries:** First/last index at 0 or `n-1`.

---

## Mistakes

- Using linear search $O(N)$ when the array is already sorted.
- Forgetting to handle the "not found" case (result should be 0, not `(-1) - (-1) + 1`).
- Off-by-one errors in `last - first + 1`.
- **User mistake:** No specific note provided.

---

## Complexity

Time: $O(\log N)$ → Two independent binary searches.  
Space: $O(1)$ → Constant extra space used for pointers.

---

## Similar Problems

- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in a Sorted Array of Unknown Size](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #binarysearch #searching
- [[Binary Search]] [[Arrays]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [GeeksforGeeks - Count occurrences in a sorted array](https://www.geeksforgeeks.org/problems/count-occurences-of-number-in-sorted-array5424/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
