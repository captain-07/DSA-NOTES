---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Find Peak Element

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Meta #Google #Amazon #Microsoft #Uber #Bloomberg

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern

Modified Binary Search (Binary Search on Answer)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

Any local maximum is a valid peak. Since the array boundaries effectively drop to $-\infty$, any "uphill" slope (where `nums[i] < nums[i+1]`) is guaranteed to eventually lead to a peak, either at a local maximum or at the end of the array. This allows us to discard half of the search space at each step.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `nums[mid] < nums[mid + 1]`, search right (`left = mid + 1`). Otherwise, search left including `mid` (`right = mid`).

---

## Approach

### Brute Force
- Linear scan to find an index `i` where `nums[i] > nums[i+1]`.
- Time: O(n)
- Space: O(1)

### Optimal
- Use **Iterative Binary Search**.
- Compare `mid` with its immediate right neighbor `mid + 1`.
- If increasing (`nums[mid] < nums[mid+1]`), a peak must exist to the right.
- If decreasing (`nums[mid] > nums[mid+1]`), a peak must exist at `mid` or to its left.
- Time: O(log n)
- Space: O(1)

---

## Code (Python)

```python
class Solution:
    def findPeakElement(self, nums: list[int]) -> int:
        # Initialize pointers for the search range
        left, right = 0, len(nums) - 1
        
        while left < right:
            mid = (left + right) // 2
            
            # Check the slope: if nums[mid] is less than the next element,
            # we are currently in an 'increasing' part. 
            # A peak must exist to the right.
            if nums[mid] < nums[mid + 1]:
                left = mid + 1
            else:
                # If nums[mid] > nums[mid + 1], we are in a 'decreasing' part.
                # A peak must exist at mid or to its left.
                right = mid
        
        # When left == right, we've converged on a peak element
        return left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 1, 3, 5, 6, 4]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `L=0, R=6, M=3` | `nums[3]=3 < nums[4]=5`. Slope is increasing. Peak is on the right. `L = 4`. |
| 2 | `L=4, R=6, M=5` | `nums[5]=6 > nums[6]=4`. Slope is decreasing. Peak is at `M` or left. `R = 5`. |
| 3 | `L=4, R=5, M=4` | `nums[4]=5 < nums[5]=6`. Slope is increasing. Peak is on the right. `L = 5`. |
| 4 | `L=5, R=5` | `L == R`. Loop terminates. Return index 5 (value 6 is a peak). |

---

## Edge Cases

- **Single Element:** `[1]` -> Binary search correctly returns index 0.
- **Strictly Increasing:** `[1, 2, 3]` -> Always moves `left` rightward, returns index 2.
- **Strictly Decreasing:** `[3, 2, 1]` -> Always moves `right` leftward, returns index 0.
- **Minimum Size:** `[1, 2]` -> `mid` is 0, `nums[0] < nums[1]`, returns index 1.

---

## Mistakes

- None.
- Returning the peak value instead of the index.
- Over-complicating the search by checking both `mid-1` and `mid+1`, which requires extra boundary handling.
- Using `left <= right` with `mid + 1` can cause out-of-bounds errors if not careful.

---

## Complexity

Time: O(log n) → The search space is halved in every iteration.  
Space: O(1) → Only a few pointers are used.

---

## Similar Problems

- [Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/) - Easy
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Find Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/) - Hard
- [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Arrays]]
  - Revision Date: 2026-04-10
  - **Problem Link:** [LeetCode - Find Peak Element](https://leetcode.com/problems/find-peak-element/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
