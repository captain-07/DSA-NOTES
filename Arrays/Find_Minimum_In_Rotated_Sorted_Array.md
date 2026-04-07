---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Find Minimum In Rotated Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Uber #GoldmanSachs

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #divideandconquer [[Divide and Conquer]]

---
## Pattern

Modified Binary Search (Inflection Point Detection)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

In a rotated sorted array, the "inflection point" (where the order breaks) is the minimum element. We use **Binary Search** to compare `nums[mid]` with `nums[right]` to decide which half to discard. Unlike standard search, we don't discard `mid` if it could be the minimum.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `nums[mid] > nums[right]`, the left side is sorted and the minimum **must** be to the right of `mid`. Otherwise, the right side is sorted and `mid` itself could be the minimum.

---

## Approach

### Brute Force
- Iterate through the entire array and track the minimum element found.
- **Time Complexity:** O(N)

### Optimal (Binary Search)
1. Initialize `left = 0`, `right = n - 1`.
2. While `left < right`:
   - Calculate `mid`.
   - If `nums[mid] > nums[right]`: The minimum is in the right unsorted part. Move `left = mid + 1`.
   - Else: The right part is sorted, so `mid` could be the minimum. Move `right = mid`.
3. Return `nums[left]`.

---

## Code (Python)

```python
def findMin(nums: list[int]) -> int:
    left, right = 0, len(nums) - 1
    
    while left < right:
        mid = left + (right - left) // 2
        
        # If mid element is greater than right element, 
        # the pivot/min is in the right half (excluding mid)
        if nums[mid] > nums[right]:
            left = mid + 1
        # Otherwise, mid could be the minimum or the min is to the left
        else:
            right = mid
            
    return nums[left]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | Left (L) | Right (R) | Mid (M) | nums[M] vs nums[R] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 7 > 2 | `nums[mid] > nums[right]`: Min is on the right. `L = M + 1 = 4`. |
| 2 | 4 | 6 | 5 | 1 < 2 | `nums[mid] <= nums[right]`: `mid` could be min. `R = M = 5`. |
| 3 | 4 | 5 | 4 | 0 < 1 | `nums[mid] <= nums[right]`: `mid` could be min. `R = M = 4`. |
| 4 | 4 | 4 | - | L == R | Loop terminates. Return `nums[4]` which is **0**. |

---

## Edge Cases

- **Array Not Rotated:** `[1, 2, 3]` → `nums[mid] < nums[right]` always moves `right` towards index 0.
- **Single Element:** `[1]` → Loop condition `left < right` handles this immediately.
- **Two Elements:** `[2, 1]` → `mid` is 0, `2 > 1`, `left` becomes 1, returns `nums[1]`.
- **Rotated at Last Index:** `[2, 3, 1]` → Correctly identifies 1 as the minimum.

---

## Mistakes

- **Incorrect Boundary Update:** Using `right = mid - 1` when `nums[mid] < nums[right]`. This is wrong because `mid` itself could be the minimum.
- **Comparison with Left:** Comparing `nums[mid]` with `nums[left]` is tricky because it doesn't clearly distinguish between a rotated and non-rotated array.
- **User Mistake:** Confusing the logic of "eliminating the sorted part". In this problem, we eliminate the sorted part **only if** the minimum cannot exist there. If the right side is sorted, the minimum *could* be the first element of that sorted part (`mid`), so we don't discard `mid`.

---

## Complexity

Time: O(log N) → Standard binary search halves the search space each iteration.  
Space: O(1) → Constant space used for pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II (with duplicates)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard
- [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Arrays]] [[Divide and Conquer]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
