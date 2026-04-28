---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Search In Rotated Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Apple #Adobe #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]

## Pattern

Modified Binary Search

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

In a rotated sorted array, at any given `mid` point, at least one half (left or right) of the array is guaranteed to be strictly sorted. We identify the sorted half and check if the target lies within its bounds to decide our next search space.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the **sorted half** first. If the target is within the range of that sorted half, search there; otherwise, search the opposite half.

---

## Approach

### Brute Force
- Linear search through the array to find the target.
- Time: O(N)

### Optimal
- Use Two Pointers (`low`, `high`) for Binary Search.
- Calculate `mid`. If `nums[mid] == target`, return `mid`.
- Check if `nums[low] <= nums[mid]` (Left side is sorted).
- If left is sorted: Check if `nums[low] <= target < nums[mid]`. If yes, `high = mid - 1`, else `low = mid + 1`.
- If right is sorted: Check if `nums[mid] < target <= nums[high]`. If yes, `low = mid + 1`, else `high = mid - 1`.

---

## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        low, high = 0, len(nums) - 1
        
        while low <= high:
            mid = (low + high) // 2
            
            if nums[mid] == target:
                return mid
            
            # Identify the sorted half
            if nums[low] <= nums[mid]:  # Left half is sorted
                if nums[low] <= target < nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:  # Right half is sorted
                if nums[mid] < target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1
                    
        return -1
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`, `target = 0`

| Step | low, mid, high | nums[mid] | Comparison & Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 0, 3, 6 | 7 | `nums[0] <= 7` (Left sorted). `0` is NOT in `[4, 7)`. Move `low = 4`. |
| 2 | 4, 5, 6 | 1 | `nums[4] <= 1` (0 <= 1 is True, Left sorted). `0` is in `[0, 1)`. Move `high = 4`. |
| 3 | 4, 4, 4 | 0 | `nums[mid] == target`. Return `mid = 4`. |

---

## Edge Cases

- **Single element:** `nums = [1], target = 0` → Should return -1.
- **Not rotated:** `nums = [1, 2, 3], target = 2` → Standard binary search behavior.
- **Target at pivot:** `nums = [4, 5, 1, 2, 3], target = 1` → Handled by `nums[mid] == target`.
- **Target not present:** Returns -1 correctly after `low > high`.

---

## Mistakes

- **Incorrect Boundary Checks:** Using `<` instead of `<=` when checking the sorted half or the target range.
- **Pivot Confusion:** Trying to find the pivot element first (O(log N)) and then doing binary search (O(log N)). While correct, the one-pass approach is cleaner.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Traditional binary search halves the search space each step.
Space: O(1) → Only constant extra space for pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Arrays]]
  - Revision Date: 2026-04-10
  - **Problem Link:** [LeetCode - Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
