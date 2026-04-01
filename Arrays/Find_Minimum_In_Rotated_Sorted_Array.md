---
created: 2026-04-01
revisions:
  - 2026-04-03
  - 2026-04-08
  - 2026-04-16
  - 2026-05-01
---

# Find Minimum In Rotated Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #modifiedbinarysearch [[Modified Binary Search]]

---
## Pattern

Modified Binary Search (Search Space Reduction)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

In a rotated sorted array, the "pivot" (minimum element) is the only point where the property `nums[i] < nums[i-1]` holds. By comparing `nums[mid]` with `nums[right]`, we can determine if the right half is sorted. If `nums[mid] > nums[right]`, the minimum **must** be in the right unsorted part. Otherwise, it is in the left part (including `mid`).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `mid` with `right`: If `nums[mid] > nums[right]`, move `left = mid + 1`. Else, `right = mid`.

---

## Approach

### Brute Force
- Linear scan through the array to find the smallest element.
- **Time:** $O(N)$

### Optimal
- Use **Binary Search**.
- Maintain `left` and `right` pointers.
- Calculate `mid`.
- If `nums[mid] > nums[right]`, the left side is sorted and the rotation point (minimum) is to the right.
- If `nums[mid] < nums[right]`, the right side is sorted, so the minimum is at `mid` or to its left.
- **Time:** $O(\log N)$

---

## Code (Python)

```python
def findMin(nums):
    left, right = 0, len(nums) - 1
    
    while left < right:
        mid = left + (right - left) // 2
        
        # If mid element is greater than right element, 
        # the min must be in the right half (mid+1 to right)
        if nums[mid] > nums[right]:
            left = mid + 1
        # If mid element is less than or equal to right element, 
        # the min is at mid or in the left half (left to mid)
        else:
            right = mid
            
    return nums[left]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 1, 2, 3]`

| Step | left | right | mid | nums[mid] vs nums[right] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 4 | 2 | `1 < 3` | `nums[mid] <= nums[right]`, so `right = mid` (2) |
| 2 | 0 | 2 | 1 | `5 > 1` | `nums[mid] > nums[right]`, so `left = mid + 1` (2) |
| 3 | 2 | 2 | - | `left == right` | Loop terminates. Result is `nums[2] = 1`. |

---

## Edge Cases

- **No Rotation:** `[1, 2, 3, 4, 5]` → `nums[mid]` is always `< nums[right]`, `right` keeps moving left until index 0.
- **Single Element:** `[1]` → Loop `while left < right` doesn't execute, returns `nums[0]`.
- **Two Elements:** `[2, 1]` → `mid` is 0, `nums[0] > nums[1]`, `left` becomes 1, returns `nums[1]`.
- **Rotated at last index:** `[2, 3, 4, 5, 1]` → Correctly identifies `1` as minimum.

---

## Mistakes

- **Incorrect Boundary Elimination:** Mistakenly eliminating the unsorted part when you should be moving toward it.
- **Using `nums[left]`:** Comparing `mid` with `left` is tricky because a non-rotated array and a rotated array can look similar from the left perspective. Always compare with `right`.
- **Loop Condition:** Using `left <= right` with `right = mid` can cause an infinite loop. Use `left < right`.
- **User Mistake:** Confusing the logic of "eliminating the sorted part". In this problem, we eliminate the sorted part **only if** the minimum cannot exist there. If the right side is sorted, the minimum *could* be the first element of that sorted part (`mid`), so we don't discard `mid`.

---

## Complexity

- **Time:** $O(\log N)$ → Each step halves the search space.
- **Space:** $O(1)$ → Only pointers are stored.

---

## Tags and Properties

- #dsa #important #revisit #binarysearch 
- [[Binary Search]] [[Arrays]] [[Search Space Reduction]]
- **Revision Date:** April 1, 2026
- **Problem Link:** [LeetCode 153](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-03)
- [ ] Day 7 Revision (2026-04-08)
- [ ] Day 15 Revision (2026-04-16)
- [ ] Day 30 Revision (2026-05-01)
