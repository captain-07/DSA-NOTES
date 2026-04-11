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

Modified Binary Search (Pivot Detection)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

In a rotated sorted array, one half is always sorted. By comparing the middle element with the rightmost element, we can determine if the minimum lies in the left or right half: if `nums[mid] > nums[right]`, the inflection point (and the minimum) must be to the right of `mid`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `nums[mid] > nums[right]`, search right (`left = mid + 1`); otherwise, search left including mid (`right = mid`).

---

## Approach

### Brute Force
- Linear scan through the array to find the smallest element.
- Time: O(N), Space: O(1)

### Better
- Find the "pivot" point where `nums[i] > nums[i+1]`. The element `nums[i+1]` is the minimum.
- Time: O(N) in worst case (not much better than brute force), Space: O(1)

### Optimal
- Use Binary Search with `left` and `right` pointers.
- Calculate `mid`.
- If `nums[mid] > nums[right]`, it means the rotation point is further right. Set `left = mid + 1`.
- If `nums[mid] <= nums[right]`, the minimum is either at `mid` or to its left. Set `right = mid`.
- The loop terminates when `left == right`.

---

## Code (Python)

```python
class Solution:
    def findMin(self, nums: list[int]) -> int:
        left, right = 0, len(nums) - 1
        
        while left < right:
            mid = left + (right - left) // 2
            
            # If mid element is greater than right element, 
            # the minimum must be in the right half.
            if nums[mid] > nums[right]:
                left = mid + 1
            # Otherwise, the minimum is in the left half (including mid).
            else:
                right = mid
                
        return nums[left]
```

---

## Dry Run (Smart Example)

Input: `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | left | right | mid | nums[mid] | nums[right] | Action | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 7 | 2 | `left = 4` | 7 > 2, min is in right half |
| 2 | 4 | 6 | 5 | 1 | 2 | `right = 5` | 1 <= 2, min could be mid or left |
| 3 | 4 | 5 | 4 | 0 | 1 | `right = 4` | 0 <= 1, min could be mid or left |
| 4 | 4 | 4 | - | - | - | **Return 0** | `left == right`, loop terminates |

---

## Edge Cases

- **Array not rotated:** `[1, 2, 3, 4, 5]` -> `nums[mid] < nums[right]` always moves `right` to `left`.
- **Single element:** `[1]` -> `left < right` is false immediately, returns `nums[0]`.
- **Two elements:** `[2, 1]` -> `mid` is 0, `nums[0] > nums[1]`, `left` becomes 1, returns `nums[1]`.
- **Large rotation:** `[2, 3, 4, 5, 1]` -> Binary search correctly identifies `1` at the end.

---

## Mistakes

- Using `nums[mid] > nums[left]` instead of `nums[right]`. This fails when the array is not rotated.
- Setting `right = mid - 1`. This might skip the minimum element if `mid` was actually the minimum.
- Incorrect loop condition (e.g., `left <= right` with `right = mid` can lead to infinite loops).
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Standard binary search reduces the search space by half each step.  
Space: O(1) → Only a few pointers are used.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II (with duplicates)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard
- [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #arrays #pivot
  - [[Binary Search]] [[Arrays]]
  - Revision Date: 2026-04-11
  - **Problem Link:** [LeetCode - Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Uber #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
