---
created: 2026-08-05
revisions:
  - 2026-08-07
  - 2026-08-12
  - 2026-08-20
  - 2026-09-04
---

# Trapping Rain Water

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Google #Microsoft #Meta #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #twopointers [[Two Pointers]], #array [[Array]], #dynamicprogramming [[Dynamic Programming]], #stack [[Monotonic Stack]]

## Pattern

Two Pointers + Prefix/Suffix Max Boundaries

---
## Difficulty

Hard
#hard

---
## ⚡ Key Idea (Core Insight)

The water trapped above bar `i` is determined by $\min(\text{left\_max}[i], \text{right\_max}[i]) - \text{height}[i]$.
Using two pointers meeting from both ends, we can keep track of dynamic boundaries (`left_max` and `right_max`) and calculate water volume without extra space.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Pointers move inward. Advance the pointer pointing to the smaller height because the water level is always bottlenecked by the smaller of the two boundary heights.

---
## Approach

### Brute Force
- Traverse each element and scan both left and right to find maximum heights.
- Time: $O(N^2)$ | Space: $O(1)$

### Better
- Precompute and store prefix maximums and suffix maximums in two arrays.
- Time: $O(N)$ | Space: $O(N)$

### Optimal
- Maintain `left` and `right` pointers, along with `left_max` and `right_max`.
- If `height[left] < height[right]`:
  - Update `left_max` or add `left_max - height[left]` to result, then increment `left`.
- Else:
  - Update `right_max` or add `right_max - height[right]` to result, then decrement `right`.

---
## Code (Python)

```python
class Solution:
    def trap(self, height: list[int]) -> int:
        if not height:
            return 0

        left, right = 0, len(height) - 1
        left_max, right_max = 0, 0
        water = 0

        while left < right:
            if height[left] < height[right]:
                if height[left] >= left_max:
                    left_max = height[left]
                else:
                    water += left_max - height[left]
                left += 1
            else:
                if height[right] >= right_max:
                    right_max = height[right]
                else:
                    water += right_max - height[right]
                right -= 1

        return water
```

---
## Dry Run (Smart Example)

Input: `height = [3, 0, 1, 0, 2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `l=0, r=4`, `l_max=0, r_max=0`, `water=0` | `height[0]=3 >= height[4]=2`. Process `r`. `height[r] >= r_max` $\rightarrow$ `r_max=2`. Dec `r` to 3. |
| 2 | `l=0, r=3`, `l_max=0, r_max=2`, `water=0` | `height[0]=3 >= height[3]=0`. Process `r`. `height[r] < r_max` $\rightarrow$ `water += 2-0=2`. Dec `r` to 2. |
| 3 | `l=0, r=2`, `l_max=0, r_max=2`, `water=2` | `height[0]=3 >= height[2]=1`. Process `r`. `height[r] < r_max` $\rightarrow$ `water += 2-1=3`. Dec `r` to 1. |
| 4 | `l=0, r=1`, `l_max=0, r_max=2`, `water=3` | `height[0]=3 >= height[1]=0`. Process `r`. `height[r] < r_max` $\rightarrow$ `water += 2-0=5`. Dec `r` to 0. Loop ends. |

Total Trapped Water: 5

---
## Edge Cases

- **Fewer than 3 bars:** `height = []` or `[1, 2]` $\rightarrow$ Returns 0 immediately.
- **Monotonic heights (no basin):** `[1, 2, 3, 4]` or `[4, 3, 2, 1]` $\rightarrow$ Returns 0.
- **Flat heights:** `[2, 2, 2]` $\rightarrow$ Returns 0.
- **High side peaks with central dip (Valley):** `[4, 0, 4]` $\rightarrow$ Correctly traps 4 units.

---
## Mistakes

- **User Mistake:** Believing the optimal two-pointer approach is crazy or counterintuitive. (Remember: we don't need the true global maximum, just the bounding maximum from the current pointer's side. The outer boundary is guaranteed by the larger pointer's element).
- **Off-by-one errors:** Incrementing or decrementing pointers before calculating the water volume.
- **Condition swap:** Moving the pointer pointing to the larger height instead of the smaller height.

---
## Complexity

Time: O(N) $\rightarrow$ Single pass through the array with two pointers.
Space: O(1) $\rightarrow$ Constant memory usage.

---
## Similar Problems

- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) - Medium
- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) - Medium
- [Trapping Rain Water II](https://leetcode.com/problems/trapping-rain-water-ii/) - Hard

---
## Tags and Properties

- #dsa #important #revisit
- #twopointers [[Two Pointers]] #array [[Array]]
- **Revision Date:** 2026-08-05
- **Problem Link:** [LeetCode - Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-07)
- [ ] Day 7 Revision (2026-08-12)
- [ ] Day 15 Revision (2026-08-20)
- [ ] Day 30 Revision (2026-09-04)
