---
created: 2026-03-31
revisions:
  - 2026-04-02
  - 2026-04-07
  - 2026-04-15
  - 2026-04-30
---

# Find First And Last Position Of Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #LinkedIn #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Array]]

## Pattern

Modified Binary Search (Two Passes)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Since the array is sorted, use **Binary Search** twice. Instead of stopping when `nums[mid] == target`, record the index as a potential candidate and continue searching in the left half (for first position) or right half (for last position).

---

## ⚡ Quick Recall (VERY IMPORTANT)

To find **First**: If `mid == target`, set `first = mid` and move `high = mid - 1`.  
To find **Last**: If `mid == target`, set `last = mid` and move `low = mid + 1`.

---

## Approach

### Brute Force
- Linear scan from left to find the first occurrence, then linear scan from right to find the last.
- Time: O(N)

### Optimal
1. **Find First Position**: Run Binary Search. If `target` is found, update `result[0]` and shrink search space to the left (`high = mid - 1`) to see if an earlier occurrence exists.
2. **Reset Pointers**: Reset `low` to 0 and `high` to `n-1`.
3. **Find Last Position**: Run Binary Search. If `target` is found, update `result[1]` and shrink search space to the right (`low = mid + 1`) to see if a later occurrence exists.
- Time: O(log N)

---

## Code (Python)

```python
def searchRange(nums, target):
    def findBound(isFirst):
        low, high = 0, len(nums) - 1
        bound = -1
        
        while low <= high:
            mid = (low + high) // 2
            
            if nums[mid] == target:
                bound = mid
                if isFirst:
                    high = mid - 1 # Look left
                else:
                    low = mid + 1  # Look right
            elif nums[mid] < target:
                low = mid + 1
            else:
                high = mid - 1
        return bound

    return [findBound(True), findBound(False)]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [5, 7, 7, 8, 8, 10]`, `target = 8`

| Pass | Step | low, high, mid | nums[mid] | Action | Result Variable |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **First** | 1 | L:0, H:5, M:2 | 7 | 7 < 8, low = mid + 1 (3) | first = -1 |
| **First** | 2 | L:3, H:5, M:4 | 8 | 8 == 8, first = 4, high = 3 | first = 4 |
| **First** | 3 | L:3, H:3, M:3 | 8 | 8 == 8, first = 3, high = 2 | first = 3 |
| **Last** | 1 | L:0, H:5, M:2 | 7 | 7 < 8, low = mid + 1 (3) | last = -1 |
| **Last** | 2 | L:3, H:5, M:4 | 8 | 8 == 8, last = 4, low = 5 | last = 4 |
| **Last** | 3 | L:5, H:5, M:5 | 10 | 10 > 8, high = 4 | last = 4 |

---

## Edge Cases

- **Empty Array**: `nums = []` -> Return `[-1, -1]`.
- **Target Not Present**: `nums = [1, 2, 4], target = 3` -> Return `[-1, -1]`.
- **Single Element**: `nums = [5], target = 5` -> Return `[0, 0]`.
- **All Elements are Target**: `nums = [8, 8, 8], target = 8` -> Return `[0, 2]`.

---

## Mistakes

- **User Mistake**: Forgetting to reset `low` and `high` pointers to original bounds before starting the second binary search pass.
- Not handling the `nums = []` case, leading to index errors.
- Using `while low < high` instead of `low <= high`, missing the last element.
- Returning `[mid, mid]` immediately upon finding the target once.

---

## Complexity

Time: O(log N) → Two independent binary searches are performed.  
Space: O(1) → Only a few variables used for pointers and results.

---

## Tags and Properties
- #dsa #important #revisit #leetcode34
- [[Binary Search]] [[Array]]
- Revision Date: 2026-03-31
- Related: [[Search in Rotated Sorted Array]], [[Find Minimum in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-02)
- [ ] Day 7 Revision (2026-04-07)
- [ ] Day 15 Revision (2026-04-15)
- [ ] Day 30 Revision (2026-04-30)
