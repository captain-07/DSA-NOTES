---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Count Occurance In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Samsung #TCS

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]], #searching [[Searching]]

---
## Pattern

Binary Search (Modified)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The array is **sorted**, which allows using **Binary Search** to find the boundaries of the target. The total count is simply the difference between the **last occurrence** index and the **first occurrence** index plus one.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find `first_occurrence` and `last_occurrence` using Binary Search; `Count = Last - First + 1`.

---

## Approach

### Brute Force
- Linear scan the array and increment a counter whenever the target is found.
- **Time Complexity:** O(N)

### Optimal
- Use two separate Binary Search functions:
  1. `findFirst`: Standard binary search, but when `arr[mid] == target`, continue searching in the left half (`high = mid - 1`) to find the leftmost index.
  2. `findLast`: Standard binary search, but when `arr[mid] == target`, continue searching in the right half (`low = mid + 1`) to find the rightmost index.
- If the first occurrence is -1, the target isn't present; return 0.
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
def count_occurrences(arr, n, x):
    def find_first(arr, n, x):
        low, high = 0, n - 1
        first = -1
        while low <= high:
            mid = (low + high) // 2
            if arr[mid] == x:
                first = mid
                high = mid - 1 # Look left
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1
        return first

    def find_last(arr, n, x):
        low, high = 0, n - 1
        last = -1
        while low <= high:
            mid = (low + high) // 2
            if arr[mid] == x:
                last = mid
                low = mid + 1 # Look right
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1
        return last

    first = find_first(arr, n, x)
    if first == -1: return 0
    
    last = find_last(arr, n, x)
    return last - first + 1
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 2, 2, 2, 3]`, `target = 2`, `n = 6`

| Step | Operation | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `find_first` | `low=0, high=5, mid=2` | `arr[2]=2`. Store `first=2`, move `high=1`. |
| 2 | `find_first` | `low=0, high=1, mid=0` | `arr[0]=1 < 2`. Move `low=1`. |
| 3 | `find_first` | `low=1, high=1, mid=1` | `arr[1]=2`. Store `first=1`, move `high=0`. Loop ends. |
| 4 | `find_last` | `low=0, high=5, mid=2` | `arr[2]=2`. Store `last=2`, move `low=3`. |
| 5 | `find_last` | `low=3, high=5, mid=4` | `arr[4]=2`. Store `last=4`, move `low=5`. |
| 6 | `find_last` | `low=5, high=5, mid=5` | `arr[5]=3 > 2`. Move `high=4`. Loop ends. |
| 7 | Result | `4 - 1 + 1 = 4` | Total occurrences of 2 is 4. |

---

## Edge Cases

- **Target not in array:** `findFirst` returns -1, function returns 0.
- **Array size 0:** Loop doesn't execute, returns 0.
- **All elements are target:** `first` is 0, `last` is `n-1`, returns `n`.
- **Target at ends:** Handled correctly by boundary conditions of Binary Search.

---

## Mistakes

- Using linear scan instead of binary search in an interview (loses points for efficiency).
- Forgetting to handle the "not found" case (if `first == -1`).
- Incorrectly updating `low` or `high` when `arr[mid] == target`.
- **User Mistake:** None.

---

## Complexity

Time: O(log N) → Two binary search passes each taking logarithmic time.  
Space: O(1) → Constant space used for pointers and variables.

---

## Similar Problems

- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Search in a Sorted Array of Unknown Size](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #searching #interview-prep
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [GeeksforGeeks - Count occurrences in a sorted array](https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
