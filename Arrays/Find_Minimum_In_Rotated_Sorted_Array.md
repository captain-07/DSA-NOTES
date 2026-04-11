---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Find Minimum In Rotated Sorted Array

---

## Pattern

Binary Search on Modified Sorted Array (Pivot Detection)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The minimum element is the only element in the array where the property `nums[i] < nums[i-1]` holds. In a rotated sorted array, the "unsorted" half always contains the minimum. If `nums[mid] > nums[right]`, the rotation point (and the minimum) must be in the right half.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `nums[mid]` with `nums[right]`. If `nums[mid] > nums[right]`, the minimum is strictly to the right (`left = mid + 1`). Otherwise, it is at `mid` or to its left (`right = mid`).

---

## Approach

### Brute Force
- Perform a linear scan of the array to find the smallest element.
- Time: O(N) | Space: O(1)

### Better
- Check if the array is already sorted (`nums[0] < nums[-1]`). If so, return `nums[0]`. Otherwise, use linear search to find the first element that is smaller than its predecessor.
- Time: O(N) | Space: O(1)

### Optimal
- Use **Binary Search**. Initialize `left = 0` and `right = n - 1`.
- While `left < right`:
    1. Calculate `mid = left + (right - left) // 2`.
    2. If `nums[mid] > nums[right]`, the pivot/minimum is in the right half: `left = mid + 1`.
    3. Else, the minimum is in the left half or is the `mid` itself: `right = mid`.
- After the loop, `left` points to the minimum element.
- Time: O(log N) | Space: O(1)

---

## Code (Python)

```python
class Solution:
    def findMin(self, nums: list[int]) -> int:
        # Initialize boundaries
        left, right = 0, len(nums) - 1
        
        # Binary search loop
        while left < right:
            mid = left + (right - left) // 2
            
            # If mid element is greater than rightmost, 
            # the minimum must be in the right (unsorted) part.
            if nums[mid] > nums[right]:
                left = mid + 1
            # Otherwise, mid could be the minimum or min is to the left.
            else:
                right = mid
        
        # When left == right, we've converged on the minimum.
        return nums[left]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `L=0, R=6, M=3` | `nums[3]=7`. `7 > nums[6]=2`. Min in right half. `L = 3 + 1 = 4`. |
| 2 | `L=4, R=6, M=5` | `nums[5]=1`. `1 <= nums[6]=2`. Min could be `M` or left. `R = 5`. |
| 3 | `L=4, R=5, M=4` | `nums[4]=0`. `0 <= nums[5]=1`. Min could be `M` or left. `R = 4`. |
| 4 | `L=4, R=4` | `L < R` is false. Return `nums[4]` which is `0`. |

---

## Edge Cases

- **Single Element:** `[1]` -> Handled by loop condition (returns immediately).
- **Two Elements (Sorted):** `[1, 2]` -> `nums[0] < nums[1]`, `right` becomes `0`, returns `nums[0]`.
- **Two Elements (Rotated):** `[2, 1]` -> `nums[0] > nums[1]`, `left` becomes `1`, returns `nums[1]`.
- **Fully Sorted (No Rotation):** `[1, 2, 3]` -> Always moves `right` until it hits `0`.
- **Max Rotation:** `[2, 3, 4, 5, 1]` -> Binary search correctly identifies `1` at the end.

---

## Mistakes

- No specific note provided.
- Comparing `nums[mid]` with `nums[left]` instead of `nums[right]`. (Fails on sorted arrays).
- Using `while left <= right`. (Can lead to index out of bounds or infinite loops if `right = mid` logic is used).
- Forgetting that the array only contains unique elements (for this specific version of the problem).

---

## Complexity

Time: O(log N) → Each step halves the search space.  
Space: O(1) → Only a few pointers used regardless of input size.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard
- [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) - Medium
- [Find Peak Element](https://leetcode.com/problems/find-peak-element/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #arrays #rotatedarray
  - [[Binary Search]] [[Arrays]]
  - Revision date: 2026-04-11
  - **Problem Link:** [LeetCode - Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Uber #Apple #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #modifiedbinarysearch [[Modified Binary Search]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
