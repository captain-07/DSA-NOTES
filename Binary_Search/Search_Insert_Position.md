---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Search Insert Position

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Adobe #Apple #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern

Binary Search (Lower Bound / Search Space Reduction)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- Perform a standard binary search on a sorted array.
- If the target isn't found, the `left` pointer (or `low`) naturally concludes at the index where the target *should* be inserted to maintain sorted order.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Binary Search: If `target` not found, `return left`.

---

## Approach

### Brute Force
- Linear search through the array until `nums[i] >= target`.
- Time: O(n)

### Optimal
- Use `left` and `right` pointers. Calculate `mid`.
- If `nums[mid] == target`, return `mid`.
- If `nums[mid] < target`, move `left = mid + 1`.
- If `nums[mid] > target`, move `right = mid - 1`.
- Return `left` if loop terminates without finding target.
- Time: O(log n)

---

## Code (Python)

```python
class Solution:
    def searchInsert(self, nums: list[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
                
        # If target is not found, 'left' is the insertion index
        return left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 3, 5, 6]`, `target = 2`

| Step | left | right | mid | nums[mid] | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 3 | 1 | 3 | `3 > 2` → `right = mid - 1` (0) |
| 2 | 0 | 0 | 0 | 1 | `1 < 2` → `left = mid + 1` (1) |
| 3 | 1 | 0 | - | - | `left > right` → Loop ends. |
| Result | - | - | - | - | **Return left (1)** |

---

## Edge Cases

- **Target smaller than all elements:** `left` remains 0.
- **Target larger than all elements:** `left` moves to `len(nums)`.
- **Empty array:** (Not possible per LC constraints, but would return 0).
- **Array with one element:** Correctly handles `target <`, `target >`, or `target ==`.

---

## Mistakes

- Using `right = mid` instead of `right = mid - 1` (can lead to infinite loops).
- Returning `mid` instead of `left` after the loop.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log n) → Binary search halves the search space each step.  
Space: O(1) → Only constant extra space for pointers.

---

## Similar Problems

- [Binary Search](https://leetcode.com/problems/binary-search/) - Easy
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #arrays #searching
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Search Insert Position](https://leetcode.com/problems/search-insert-position/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
