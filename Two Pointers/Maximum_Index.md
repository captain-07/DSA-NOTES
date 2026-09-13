---
created: 2026-09-13
revisions:
  - 2026-09-15
  - 2026-09-20
  - 2026-09-28
  - 2026-10-13
---

# Maximum Index

---

## Metadata & Placement Tags

- **Folder:** Two Pointers
- **Target Companies:** #Amazon #Microsoft #MakeMyTrip #VMTware
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [x] High

- **Concepts:**
  - #twopointers [[Two Pointers]], #precomputation [[Precomputation]], #arrays [[Arrays]]

## Pattern

Precomputation (Prefix Min & Suffix Max) + Two Pointers

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- Maintain `LMin[i]` storing the minimum element from index `0` to `i` and `RMax[j]` storing the maximum element from index `j` to `n-1`.
- `LMin` is monotonically non-increasing and `RMax` is monotonically non-increasing from right to left, allowing a **Two-Pointers scan** on both arrays to find the maximum `j - i` in linear time.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Build `LMin` (left-to-right minimums) and `RMax` (right-to-left maximums).
- Advance `right` pointer if `LMin[left] <= RMax[right]`, updating `max_diff = max(max_diff, right - left)`; otherwise, advance `left`.

---

## Approach

### Brute Force
- Check all pairs `(i, j)` where `i <= j` and `arr[i] <= arr[j]`, keeping track of maximum `j - i`.
- Time: O(N²), Space: O(1)

### Optimal (Precomputed Min/Max Arrays + Two Pointers)
1. Precompute `LMin` where `LMin[i] = min(arr[0...i])`.
2. Precompute `RMax` where `RMax[j] = max(arr[j...n-1])`.
3. Initialize `left = 0`, `right = 0`, `max_diff = 0`.
4. Traverse using two pointers: if `LMin[left] <= RMax[right]`, increment `right` to maximize distance; else, increment `left` to relax condition.
- Time: O(N), Space: O(N)

---

## Code (Python)

```python
class Solution:
    def maxIndexDiff(self, arr: list[int]) -> int:
        n = len(arr)
        if n <= 1:
            return 0

        # LMin[i] stores the minimum value from arr[0] to arr[i]
        left_min = [0] * n
        left_min[0] = arr[0]
        for i in range(1, n):
            left_min[i] = min(arr[i], left_min[i - 1])

        # RMax[j] stores the maximum value from arr[j] to arr[n-1]
        right_max = [0] * n
        right_max[n - 1] = arr[n - 1]
        for j in range(n - 2, -1, -1):
            right_max[j] = max(arr[j], right_max[j + 1])

        # Two pointers traversal on left_min and right_max
        left = 0
        right = 0
        max_diff = 0

        while left < n and right < n:
            if left_min[left] <= right_max[right]:
                max_diff = max(max_diff, right - left)
                right += 1  # Try to find a larger distance
            else:
                left += 1   # Left minimum is too big, move left pointer forward

        return max_diff
```

---

## Dry Run (Smart Example)

Input: `arr = [34, 8, 10, 3, 2, 80, 30, 33, 1]`
`LMin = [34, 8, 8, 3, 2, 2, 2, 2, 1]`
`RMax = [80, 80, 80, 80, 80, 80, 33, 33, 1]`

| Step | Variables | Explanation |
|---|---|---|
| 1 | `left=0, right=0`, `LMin[0]=34 <= RMax[0]=80` | Valid pair! `max_diff = max(0, 0-0) = 0`. Move `right` to 1. |
| 2 | `left=0, right=5`, `LMin[0]=34 <= RMax[5]=80` | Valid pair! `max_diff = max(0, 5-0) = 5`. Move `right` to 6. |
| 3 | `left=0, right=6`, `LMin[0]=34 <= RMax[6]=30` | False (`34 > 30`). Increment `left` to 1. |
| 4 | `left=1, right=7`, `LMin[1]=8 <= RMax[7]=33` | Valid pair! `max_diff = max(5, 7-1) = 6`. Move `right` to 8. |
| 5 | `left=1, right=8`, `LMin[1]=8 <= RMax[8]=1` | False (`8 > 1`). Increment `left` to 2, 3, ... until end. |

---

## Edge Cases

- **Strictly Decreasing Array (`[5, 4, 3, 2, 1]`):** Output is `0` since `arr[i] <= arr[j]` only holds for `i == j`.
- **All Elements Equal (`[7, 7, 7, 7]`):** Output is `n - 1` (`3`).
- **Single Element Array (`[10]`):** Output is `0`.
- **Negative numbers present (`[-2, 5, -1, 3]`):** Precomputed min/max logic naturally handles sign differences.

---

## Mistakes

- Precomputing `LMin` and `RMax` is the most intuitively optimal O(N) space/time solution; trying to solve it in O(1) space without modifying array requires non-intuitive/complex binary search/stack approaches.
- Incrementing `left` instead of `right` when condition `LMin[left] <= RMax[right]` is met (blocks finding larger index gap).
- Forget to check boundary condition when `left` or `right` reaches end of array.

---

## Complexity

Time: O(N) → Single pass to build `LMin`, `RMax`, and two-pointer traversal takes O(N).
Space: O(N) → Auxiliary memory for `LMin` and `RMax` arrays of size N.

---

## Similar Problems

- [Maximum Width Ramp](https://leetcode.com/problems/maximum-width-ramp/) - Medium
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) - Medium
- [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) - Hard

---

## Tags and Properties

- #dsa #important #revisit
- #array #twopointers #precomputation
- Concept Links: [[Two Pointers]], [[Precomputation]], [[Arrays]]
- **Last Revised:** 2026-09-13
- **Problem Link:** [GeeksforGeeks - Maximum Index](https://www.geeksforgeeks.org/problems/maximum-index-1587115620/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-15)
- [ ] Day 7 Revision (2026-09-20)
- [ ] Day 15 Revision (2026-09-28)
- [ ] Day 30 Revision (2026-10-13)
