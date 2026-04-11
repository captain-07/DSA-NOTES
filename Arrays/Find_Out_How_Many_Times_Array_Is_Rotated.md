---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Find Out How Many Times Array Is Rotated

---

## Pattern

Modified Binary Search (Finding Pivot/Minimum)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The number of rotations in a sorted array is equal to the **index of the minimum element**. In a rotated sorted array, the minimum element is the only element where the previous element is greater than it (the "pivot" point).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the index of the **minimum element** using Binary Search. If `arr[mid] > arr[high]`, the pivot is in the right half; otherwise, it's in the left half (including mid).

---

## Approach

### Brute Force
- Linear search to find the minimum element's index.
- **Time Complexity:** O(N)

### Better
- Use a simple `min()` function or iterate once to find where `arr[i] < arr[i-1]`.
- **Time Complexity:** O(N)

### Optimal
- Use **Binary Search** to find the pivot.
- Compare `arr[mid]` with `arr[high]`.
- If `arr[mid] > arr[high]`, the left part is sorted, and the minimum must be to the right of `mid` (`low = mid + 1`).
- Otherwise, `mid` could be the minimum or it's to the left (`high = mid`).
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
class Solution:
    def findKRotation(self, nums: list[int]) -> int:
        """
        Finds the number of times a sorted array has been rotated.
        The count is equal to the index of the minimum element.
        """
        low, high = 0, len(nums) - 1
        
        # Binary Search to find the index of the minimum element
        while low < high:
            mid = low + (high - low) // 2
            
            # If mid element is greater than the last element, 
            # the pivot (minimum) is in the right half.
            if nums[mid] > nums[high]:
                low = mid + 1
            # Otherwise, the minimum is in the left half (including mid).
            else:
                high = mid
                
        # 'low' will point to the index of the minimum element
        return low
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | low | high | mid | `nums[mid]` vs `nums[high]` | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | `7 > 2` (True) | `low = 4` |
| 2 | 4 | 6 | 5 | `1 > 2` (False) | `high = 5` |
| 3 | 4 | 5 | 4 | `0 > 1` (False) | `high = 4` |
| 4 | 4 | 4 | - | `low == high` | **Return 4** |

---

## Edge Cases

- **No rotation:** `[1, 2, 3]` returns `0`.
- **Single element:** `[1]` returns `0`.
- **Rotated once:** `[3, 1, 2]` returns `1`.
- **Duplicates:** Standard binary search might need O(N) in worst-case (e.g., `[2, 2, 2, 0, 2]`).

---

## Mistakes

- Bullet points only
- Direct and actionable
- Confusing "number of rotations" with the "value of the minimum element".
- Not handling the case where the array is already sorted (0 rotations).
- Using `mid + 1` or `mid - 1` incorrectly, causing an infinite loop or skipping the minimum.
- **User mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Binary search halves the search space in each step.  
Space: O(1) → Only a few pointers are used.

---

## Similar Problems

- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #arrays #pivot
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-11
  - **Problem Link:** [GeeksforGeeks - Rotation Count](https://www.geeksforgeeks.org/problems/rotation4523/1)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #Google #Flipkart

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
