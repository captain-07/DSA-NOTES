---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Find First And Last Position Of Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Facebook #Amazon #Microsoft #LinkedIn #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]]

## Pattern

Modified Binary Search (Finding Boundaries)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The array is sorted, which signals **Binary Search**. To find the range, perform two separate binary searches: one to find the **leftmost** index and another for the **rightmost** index. When `nums[mid] == target`, don't stop; adjust the search range to keep looking for a "more extreme" boundary.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Run Binary Search twice. If `nums[mid] == target`, record the index and move `right = mid - 1` (to find first) or `left = mid + 1` (to find last).

---

## Approach

### Brute Force
- Linear scan through the array to find the first and last occurrence.
- **Time Complexity:** O(N)

### Optimal
- **Two Binary Searches:** 
    1. First search: If `target` is found, update `first_idx` and move `right` pointer to `mid - 1` to check the left side.
    2. Second search: If `target` is found, update `last_idx` and move `left` pointer to `mid + 1` to check the right side.
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
def searchRange(nums, target):
    def findBound(is_first):
        left, right = 0, len(nums) - 1
        bound = -1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if nums[mid] == target:
                bound = mid
                if is_first:
                    # Look left for earlier occurrence
                    right = mid - 1
                else:
                    # Look right for later occurrence
                    left = mid + 1
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        return bound

    return [findBound(True), findBound(False)]
```

---

## Dry Run (Smart Example)

Input: `nums = [5, 7, 7, 8, 8, 10]`, `target = 8`

**Finding First Position (`is_first = True`):**

| Step | left, right | mid | nums[mid] | Action | bound |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0, 5 | 2 | 7 | 7 < 8, `left = 3` | -1 |
| 2 | 3, 5 | 4 | 8 | 8 == 8, `bound = 4`, `right = 3` | 4 |
| 3 | 3, 3 | 3 | 8 | 8 == 8, `bound = 3`, `right = 2` | 3 |
| End | 3, 2 | - | - | Loop terminates | **3** |

---

## Edge Cases

- **Empty Array:** Should return `[-1, -1]`.
- **Target Not Present:** Binary search finishes without finding target, returns `[-1, -1]`.
- **All Elements are Target:** Should return `[0, n-1]`.
- **Single Element Array:** Returns `[0, 0]` if match, else `[-1, -1]`.

---

## Mistakes

- Using a single linear scan (O(N)) instead of binary search (O(log N)).
- Forgetting to handle the "not found" case correctly.
- Stopping the search immediately after finding the target instead of searching for boundaries.
- **User Mistake:** None

---

## Complexity

Time: O(log N) → Two independent binary searches take 2 * log N time.  
Space: O(1) → Only a few pointers and variables used.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #sorting
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-a-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
