---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Find Minimum In Rotated Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Facebook #Google #GoldmanSachs #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern

Binary Search (Modified for Rotated Sorted Array)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The array consists of two sorted segments. The minimum element is the "pivot" where the rotation occurred. By comparing `nums[mid]` with the rightmost element `nums[right]`, we can determine if the minimum lies in the left or right part of the current search space.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `nums[mid]` with `nums[right]`. If `nums[mid] > nums[right]`, search right (`left = mid + 1`). Otherwise, search left including mid (`right = mid`).

---

## Approach

### Brute Force
- Iterate through the entire array and track the minimum value.
- **Time:** O(N)
- **Space:** O(1)

### Optimal (Binary Search)
- Use two pointers `left` and `right`.
- While `left < right`:
  - Calculate `mid`.
  - If `nums[mid] > nums[right]`: The minimum must be in the unsorted right half.
  - Else: The minimum is either `mid` or in the left half.
- Return `nums[left]`.
- **Time:** O(log N)
- **Space:** O(1)

---

## Code (Python)

```python
class Solution:
    def findMin(self, nums: list[int]) -> int:
        left, right = 0, len(nums) - 1
        
        while left < right:
            mid = left + (right - left) // 2
            
            # If mid element is greater than rightmost, 
            # the minimum is in the right half.
            if nums[mid] > nums[right]:
                left = mid + 1
            # If mid element is less than or equal to rightmost,
            # the minimum is at mid or to the left.
            else:
                right = mid
                
        return nums[left]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | left | right | mid | nums[mid] | nums[right] | Action | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 7 | 2 | `left = 4` | `7 > 2`, min is in right half. |
| 2 | 4 | 6 | 5 | 1 | 2 | `right = 5` | `1 <= 2`, min could be mid or left. |
| 3 | 4 | 5 | 4 | 0 | 1 | `right = 4` | `0 <= 1`, min could be mid or left. |
| 4 | 4 | 4 | - | - | - | **End** | `left == right`, return `nums[4]` (0). |

---

## Edge Cases

- **Already Sorted:** `[1, 2, 3, 4, 5]` -> Returns index 0.
- **Single Element:** `[1]` -> Returns index 0.
- **Two Elements (Sorted):** `[1, 2]` -> Returns index 0.
- **Two Elements (Rotated):** `[2, 1]` -> Returns index 1.
- **Rotated at last index:** `[2, 3, 4, 5, 1]` -> Returns index 4.

---

## Mistakes

- **Incorrect Elimination:** Confusing the logic of "eliminating the sorted part". In this problem, we eliminate the sorted part **only if** the minimum cannot exist there. If the right side is sorted, the minimum *could* be the first element of that sorted part (`mid`), so we don't discard `mid`.
- **Using `left <= right`:** Leads to an infinite loop because `right = mid` doesn't always reduce the search space if the condition isn't carefully managed.
- **Comparing with `nums[left]`:** Comparing `mid` with `left` is unreliable because the rotation point might be anywhere; comparing with `right` provides a consistent signal for the pivot location.

---

## Complexity

Time: O(log N) → Standard binary search halves the search space each iteration.  
Space: O(1) → Only constant extra space used for pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard
- [Find Peak Element](https://leetcode.com/problems/find-peak-element/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Arrays]] [[Divide and Conquer]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
