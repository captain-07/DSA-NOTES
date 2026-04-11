---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Count Occurance In Sorted Array

---

## Pattern

Binary Search (First and Last Occurrence)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Since the array is sorted, all occurrences of the target are contiguous. Use **Binary Search** twice to find the `first` and `last` index of the target. The count is simply `last - first + 1`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the boundary indices using modified Binary Search: `Count = (LastIndex - FirstIndex + 1)`. If not found, return 0.

---

## Approach

### Brute Force
- Linearly traverse the array and increment a counter whenever the target is met.
- **Time:** O(N)

### Optimal
- Use Binary Search to find the **first occurrence** (search left if `arr[mid] == target`).
- Use Binary Search to find the **last occurrence** (search right if `arr[mid] == target`).
- If the target is found, return `last - first + 1`, otherwise return 0.
- **Time:** O(log N)

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
                high = mid - 1 # Keep searching left
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
                low = mid + 1 # Keep searching right
            elif arr[mid] < x:
                low = mid + 1
            else:
                high = mid - 1
        return res
```

---

## Dry Run (Smart Example)

Input: `arr = [1, 1, 2, 2, 2, 2, 3]`, `target = 2`

| Step | Function | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | `findFirst` | `low=0, high=6, mid=3` | `arr[3]=2`. `res=3`, `high=2`. Search left. |
| 2 | `findFirst` | `low=0, high=2, mid=1` | `arr[1]=1 < 2`. `low=2`. |
| 3 | `findFirst` | `low=2, high=2, mid=2` | `arr[2]=2`. `res=2`, `high=1`. Loop ends. First index = 2. |
| 4 | `findLast` | `low=0, high=6, mid=3` | `arr[3]=2`. `res=3`, `low=4`. Search right. |
| 5 | `findLast` | `low=4, high=6, mid=5` | `arr[5]=2`. `res=5`, `low=6`. |
| 6 | `findLast` | `low=6, high=6, mid=6` | `arr[6]=3 > 2`. `high=5`. Loop ends. Last index = 5. |
| **Result** | | `5 - 2 + 1 = 4` | Target 2 appears 4 times. |

---

## Edge Cases

- **Target not in array:** `findFirst` returns -1, function returns 0.
- **All elements are target:** `first=0`, `last=n-1`, count is `n`.
- **Target at ends:** Correctly handled by boundary updates in Binary Search.
- **Empty array:** Handled by `low <= high` condition (returns 0).

---

## Mistakes

- Using linear search $O(N)$ when the array is already sorted.
- Forgetting to handle the case where the target doesn't exist (returning `0 - (-1) + 1` incorrectly).
- Incorrect `mid` calculation in languages like C++/Java (use `low + (high-low)/2`).
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Two binary search passes take $2 \times \log N$ time.  
Space: O(1) → Only a few variables used for pointers and indices.

---

## Similar Problems

- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #array #count-occurrences
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-11
  - **Problem Link:** [GeeksforGeeks - Count occurrences in a sorted array](https://www.geeksforgeeks.org/problems/count-occurences-of-a-number-in-a-sorted-array1520/1)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Samsung #Adobe #Google

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]], #sorting [[Sorting]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
