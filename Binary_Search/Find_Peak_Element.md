---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Find Peak Element

---

## Pattern

Binary Search (Modified) / Gradient Search

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The problem guarantees that $nums[i] \neq nums[i+1]$ and boundaries are $-\infty$. If `nums[mid] < nums[mid+1]`, you are currently on an upward slope, meaning a peak **must** exist to the right. Conversely, if `nums[mid] > nums[mid+1]`, you are on a downward slope or at a peak, so a peak **must** exist to the left (including `mid`).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `nums[mid]` with `nums[mid+1]`. Move towards the **higher** neighbor. Since boundaries are $-\infty$, "climbing up" always leads to a peak.

---

## Approach

### Brute Force
- Linear scan through the array to find the first element that is greater than its next neighbor.
- **Time Complexity:** $O(n)$

### Optimal (Binary Search)
1. Initialize `left = 0`, `right = len(nums) - 1`.
2. While `left < right`:
   - Calculate `mid`.
   - If `nums[mid] < nums[mid + 1]`, the peak is in the right half: `left = mid + 1`.
   - Else, the peak is at `mid` or to the left: `right = mid`.
3. Return `left` (or `right`), as they converge on a peak.

---

## Code (Python)

```python
class Solution:
    def findPeakElement(self, nums: list[int]) -> int:
        left, right = 0, len(nums) - 1
        
        while left < right:
            mid = left + (right - left) // 2
            
            # If mid is less than the next element, peak is to the right
            if nums[mid] < nums[mid + 1]:
                left = mid + 1
            # Otherwise, mid could be a peak or peak is to the left
            else:
                right = mid
                
        return left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 1, 3, 5, 6, 4]`

| Step | Variables (L, R, M) | Explanation |
| :--- | :--- | :--- |
| 1 | L=0, R=6, M=3 | `nums[3]=3 < nums[4]=5`. Peak is right. L = M+1 = 4. |
| 2 | L=4, R=6, M=5 | `nums[5]=6 > nums[6]=4`. Peak is left/at M. R = M = 5. |
| 3 | L=4, R=5, M=4 | `nums[4]=5 < nums[5]=6`. Peak is right. L = M+1 = 5. |
| 4 | L=5, R=5 | Loop ends. Return L = 5 (Element 6). |

---

## Edge Cases

- **Single Element:** `[1]` → Loop never starts, returns index 0.
- **Strictly Increasing:** `[1, 2, 3]` → Binary search pushes `left` to the last index.
- **Strictly Decreasing:** `[3, 2, 1]` → Binary search pushes `right` to the first index.
- **Peak at Ends:** Handled naturally by the boundary logic and `left < right` condition.

---

## Mistakes

- **Incorrect Boundary:** Using `while left <= right` can lead to an infinite loop if not careful with `mid + 1`.
- **Index Out of Bounds:** Accessing `nums[mid+1]` when `mid` is the last index (avoided by `left < right`).
- **User Mistake:** No specific note provided. Ensure logic covers the "climb the hill" intuition for future recall.

---

## Complexity

Time: $O(\log n)$ → We halve the search space in each iteration.  
Space: $O(1)$ → Iterative approach uses constant extra space.

---

## Similar Problems

- [Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/) - Easy
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #binarysearch #gradient-descent
- [[Binary Search]] [[Array]]
- **Revision Date:** 2026-04-11
- **Problem Link:** [LeetCode - Find Peak Element](https://leetcode.com/problems/find-peak-element/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Facebook #Amazon #Microsoft #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]]

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
