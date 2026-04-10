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
  - #Amazon #Google #Microsoft #Facebook #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]]

## Pattern

Modified Binary Search (Search on Answer)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The problem guarantees $nums[i] \neq nums[i+1]$. If $nums[mid] < nums[mid+1]$, an ascending slope exists, ensuring a peak lies to the **right**. Conversely, if $nums[mid] > nums[mid+1]$, a peak exists at or to the **left**.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `nums[mid]` with `nums[mid+1]`. If increasing, `left = mid + 1`; else `right = mid`.

---

## Approach

### Brute Force
- Linear scan through the array to find the first element $i$ such that $nums[i] > nums[i+1]$.
- Time: $O(N)$

### Optimal
- Use **Binary Search** to achieve logarithmic time.
- 1. Initialize `left = 0`, `right = len(nums) - 1`.
- 2. While `left < right`, calculate `mid`.
- 3. If `nums[mid] < nums[mid+1]`, the peak is in the right half (`left = mid + 1`).
- 4. Otherwise, the peak is in the left half including `mid` (`right = mid`).
- 5. Return `left` (or `right`) as the index.

---

## Code (Python)

```python
class Solution:
    def findPeakElement(self, nums: list[int]) -> int:
        left, right = 0, len(nums) - 1
        
        while left < right:
            mid = left + (right - left) // 2
            
            # If we are on an upward slope, the peak is to the right
            if nums[mid] < nums[mid+1]:
                left = mid + 1
            # If we are on a downward slope, mid could be the peak or peak is to the left
            else:
                right = mid
                
        return left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 1, 3, 5, 6, 4]`

| Step | Variables (L, R, M) | Explanation |
| :--- | :--- | :--- |
| 1 | L=0, R=6, M=3 | `nums[3]=3`, `nums[4]=5`. `3 < 5` (Upward). `L = M + 1 = 4`. |
| 2 | L=4, R=6, M=5 | `nums[5]=6`, `nums[6]=4`. `6 > 4` (Downward). `R = M = 5`. |
| 3 | L=4, R=5, M=4 | `nums[4]=5`, `nums[5]=6`. `5 < 6` (Upward). `L = M + 1 = 5`. |
| 4 | L=5, R=5 | `L == R`. Loop terminates. Return `L = 5` (Element 6). |

---

## Edge Cases

- **Single Element:** `[1]` → Returns index 0.
- **Strictly Increasing:** `[1, 2, 3]` → Peak is at the end (index 2).
- **Strictly Decreasing:** `[3, 2, 1]` → Peak is at the start (index 0).
- **Two Elements:** `[1, 2]` → Returns index 1.

---

## Mistakes

- **Index Out of Bounds:** Ensure `mid + 1` is safe (loop condition `left < right` handles this).
- **Comparison Logic:** Don't check both neighbors; one neighbor comparison is sufficient to determine slope.
- **User Mistake:** None.

---

## Complexity

Time: O(log N) → Binary search halves the search space each step.  
Space: O(1) → Iterative approach uses constant extra space.

---

## Similar Problems

- [Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-min-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch  
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Find Peak Element](https://leetcode.com/problems/find-peak-element/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
