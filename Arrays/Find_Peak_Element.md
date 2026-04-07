---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Find Peak Element

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Facebook #Microsoft #Uber #Directi

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern

Binary Search on Answer Space (Slope Property)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The problem guarantees `nums[i] != nums[i+1]`. If you are on an upward slope (`nums[mid] < nums[mid + 1]`), a peak **must** exist to your right. If you are on a downward slope (`nums[mid] > nums[mid + 1]`), a peak **must** exist at `mid` or to your left. 

---

## ⚡ Quick Recall (VERY IMPORTANT)

"Climb the mountain": Compare `mid` with `mid + 1`. Move towards the higher neighbor to find a peak.

---

## Approach

### Brute Force
- Linear scan through the array and return the first index `i` where `nums[i] > nums[i+1]`.
- Time Complexity: O(N)

### Optimal
- Use Binary Search to find the slope direction.
- If `nums[mid] < nums[mid + 1]`, search the right half (`left = mid + 1`).
- Otherwise, search the left half including `mid` (`right = mid`).
- The loop terminates when `left == right`, pointing to a peak element.

---

## Code (Python)

```python
def findPeakElement(nums: list[int]) -> int:
    left, right = 0, len(nums) - 1
    
    while left < right:
        mid = (left + right) // 2
        
        # Check if we are on an upward slope
        if nums[mid] < nums[mid + 1]:
            # Peak is definitely to the right
            left = mid + 1
        else:
            # We are on a downward slope, mid could be the peak
            right = mid
            
    # left and right converge to the peak index
    return left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 1, 3, 5, 6, 4]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `l=0, r=6, m=3` | `nums[3]=3 < nums[4]=5`. Upward slope. Peak is on right. `l=4`. |
| 2 | `l=4, r=6, m=5` | `nums[5]=6 > nums[6]=4`. Downward slope. Peak is left/mid. `r=5`. |
| 3 | `l=4, r=5, m=4` | `nums[4]=5 < nums[5]=6`. Upward slope. Peak is on right. `l=5`. |
| 4 | `l=5, r=5` | Loop ends. `left == right`. Return index 5 (value 6). |

---

## Edge Cases

- **Single Element:** `[1]` → Returns index 0.
- **Strictly Increasing:** `[1, 2, 3]` → Returns index 2 (last element).
- **Strictly Decreasing:** `[3, 2, 1]` → Returns index 0 (first element).
- **Two Elements:** `[1, 2]` → Correctly identifies index 1.

---

## Mistakes

- **Incorrect Boundary:** Using `while left <= right` can lead to infinite loops if `right = mid` is used.
- **Neighbor Check:** Comparing `mid` with `mid - 1` without checking bounds (safer to use `mid + 1` with `left < right`).
- **User Mistake:** None

---

## Complexity

Time: O(log N) → Standard binary search reduces the search space by half each iteration.  
Space: O(1) → Constant space usage for pointers.

---

## Similar Problems

- [Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/) - Medium
- [Find a Peak Element II (2D)](https://leetcode.com/problems/find-a-peak-element-ii/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Find Peak Element](https://leetcode.com/problems/find-peak-element/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
