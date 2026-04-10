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
  - #Amazon #Google #Microsoft #Facebook #Uber #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #modifiedbinarysearch [[Modified Binary Search]]

## Pattern

Modified Binary Search (Pivot Detection)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

A rotated sorted array consists of two sorted subarrays. The minimum element is the "pivot" point where the ascending order breaks. By comparing `nums[mid]` with `nums[right]`, we can determine if the minimum lies in the left or right half.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `mid` with `right`: If `nums[mid] > nums[right]`, search right (`left = mid + 1`). Otherwise, search left including mid (`right = mid`).

---

## Approach

### Brute Force
- Iterate through the entire array to find the minimum element.
- Time Complexity: O(N)

### Optimal (Binary Search)
1. Initialize `left = 0` and `right = n - 1`.
2. While `left < right`:
   - Calculate `mid`.
   - If `nums[mid] > nums[right]`, the rotation point (and the min) must be to the right of `mid`.
   - Else, `nums[mid]` could be the minimum or the minimum is to its left.
3. Return `nums[left]`.
- Time Complexity: O(log N)

---

## Code (Python)

```python
class Solution:
    def findMin(self, nums: list[int]) -> int:
        left, right = 0, len(nums) - 1
        
        while left < right:
            mid = left + (right - left) // 2
            
            # If mid is greater than right, pivot is in the right half
            if nums[mid] > nums[right]:
                left = mid + 1
            # If mid is less than or equal to right, pivot is at mid or left
            else:
                right = mid
                
        return nums[left]
```

---

## Dry Run (Smart Example)

Input: `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `L=0, R=6, M=3` | `nums[3]=7 > nums[6]=2`. Minimum must be in the right half. `L = M + 1 = 4`. |
| 2 | `L=4, R=6, M=5` | `nums[5]=1 < nums[6]=2`. Minimum is at index 5 or to its left. `R = M = 5`. |
| 3 | `L=4, R=5, M=4` | `nums[4]=0 < nums[5]=1`. Minimum is at index 4 or to its left. `R = M = 4`. |
| 4 | `L=4, R=4` | `L == R`. Loop terminates. Result is `nums[4] = 0`. |

---

## Edge Cases

- **Single Element `[1]`**: Loop doesn't run, returns `nums[0]`.
- **Already Sorted `[1, 2, 3]`**: `nums[mid]` will always be `< nums[right]`, `right` keeps moving left until it hits index 0.
- **Rotated by 1 `[2, 3, 1]`**: Correct handles the pivot at the end.
- **Two Elements `[2, 1]`**: `mid` will be 0, `nums[0] > nums[1]`, `left` becomes 1, returns `nums[1]`.

---

## Mistakes

- Using `left <= right` with `right = mid - 1` can accidentally skip the minimum element since `mid` itself could be the minimum.
- Comparing `nums[mid]` with `nums[left]` is unreliable because it doesn't clearly distinguish which half is sorted in all rotation cases.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → The search space is halved in each iteration of the binary search.  
Space: O(1) → Only a constant amount of extra space is used for pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard
- [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #binarysearch #leetcode-medium
- [[Binary Search]] [[Arrays]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [LeetCode #153 - Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
