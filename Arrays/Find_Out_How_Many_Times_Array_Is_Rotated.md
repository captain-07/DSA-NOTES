---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Find Out How Many Times Array Is Rotated

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #GoldmanSachs #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

## Pattern

- Modified Binary Search (Finding the Pivot/Minimum element)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The number of rotations in a sorted array is equal to the **index of the minimum element**. In a sorted rotated array, the minimum element is the only element that is smaller than its previous element (the "pivot" point).

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the **index of the minimum element** using Binary Search. If `arr[mid] > arr[high]`, the min is in the right half; otherwise, it's in the left half (including mid).

---

## Approach

### Brute Force
- Linearly search for the minimum element and return its index.
- Time: O(N) | Space: O(1)

### Optimal
- Use Binary Search to find the pivot point.
- If `arr[low] <= arr[high]`, the array is not rotated (return `low`).
- Check if `mid` is the minimum by comparing with neighbors.
- Shrink the search space by comparing `arr[mid]` with `arr[high]`.
- Time: O(log N) | Space: O(1)

---

## Code (Python)

```python
def find_rotation_count(nums):
    low, high = 0, len(nums) - 1
    
    # If array is already sorted and not rotated
    if nums[low] <= nums[high]:
        return 0
        
    while low <= high:
        mid = (low + high) // 2
        
        # Check if mid+1 is the minimum element
        if mid < high and nums[mid] > nums[mid + 1]:
            return mid + 1
            
        # Check if mid itself is the minimum element
        if mid > low and nums[mid] < nums[mid - 1]:
            return mid
            
        # Decide which half to search
        if nums[mid] > nums[high]:
            # Minimum must be in the right half
            low = mid + 1
        else:
            # Minimum must be in the left half
            high = mid - 1
            
    return 0
```

---

## Dry Run (Smart Example)

Input: `nums = [4, 5, 6, 7, 0, 1, 2]`

| Step | Variables (low, mid, high) | Explanation |
| :--- | :--- | :--- |
| 1 | L:0, M:3, H:6 | `nums[3]=7`, `nums[6]=2`. Since `7 > 2`, min is in right half. `low = mid + 1 = 4`. |
| 2 | L:4, M:5, H:6 | `nums[5]=1`. Check neighbors: `nums[5] < nums[4]` (1 < 0) is false. `nums[5] > nums[6]` is false. |
| 3 | L:4, M:5, H:6 | `nums[5]=1`, `nums[6]=2`. `1 < 2`, so `high = mid - 1 = 4`. |
| 4 | L:4, M:4, H:4 | `nums[4]=0`. `mid > low` check fails. But `mid < high` also fails. Loop ends or logic returns index 4. |

*Correction:* In Step 2, if `nums[mid] < nums[mid-1]` (0 < 7), it immediately returns `mid`.

---

## Edge Cases

- **No rotation:** `[1, 2, 3, 4]` → Returns 0.
- **Single element:** `[1]` → Returns 0.
- **Rotated N-1 times:** `[2, 3, 4, 1]` → Returns 3.
- **Array with duplicates:** Requires O(N) worst case (e.g., `[1, 1, 0, 1, 1]`).

---

## Mistakes

- **Incorrect index:** Returning the minimum value instead of the index.
- **Pivot logic:** Forgetting to handle the "already sorted" case at the start.
- **User mistake:** None.

---

## Complexity

Time: O(log N) → Binary search halves the search space each iteration.  
Space: O(1) → Only a few pointers used.

---

## Similar Problems

- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II (Duplicates)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Array Rotation]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [GeeksforGeeks - Rotation Count](https://www.geeksforgeeks.org/find-rotation-count-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
