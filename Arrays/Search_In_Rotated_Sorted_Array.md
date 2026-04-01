---
created: 2026-04-01
revisions:
  - 2026-04-03
  - 2026-04-08
  - 2026-04-16
  - 2026-05-01
---

# Search In Rotated Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe #Apple

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

Modified Binary Search (Sorted Half Identification)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Even after rotation, at any given index `mid`, **at least one half** (left `[low...mid]` or right `[mid...high]`) is guaranteed to be strictly sorted. Identify the sorted half first, then check if the target resides within its bounds.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find `mid`. If `nums[low] <= nums[mid]`, left is sorted. If `nums[mid] <= nums[high]`, right is sorted. Only then check if `target` is within that sorted range.

---

## Approach

### Brute Force
- Linear search through the array to find the target.
- **Time Complexity:** O(N)

### Optimal
1. Initialize `low = 0`, `high = n - 1`.
2. While `low <= high`:
   - Calculate `mid`.
   - If `nums[mid] == target`, return `mid`.
   - **Identify Sorted Side:**
     - If `nums[low] <= nums[mid]`: Left side is sorted.
       - If `nums[low] <= target < nums[mid]`: Search left (`high = mid - 1`).
       - Else: Search right (`low = mid + 1`).
     - Else: Right side is sorted.
       - If `nums[mid] < target <= nums[high]`: Search right (`low = mid + 1`).
       - Else: Search left (`high = mid - 1`).
3. Return -1 if not found.

---

## Code (Python)

```python
def search(nums, target):
    low, high = 0, len(nums) - 1
    
    while low <= high:
        mid = (low + high) // 2
        
        if nums[mid] == target:
            return mid
        
        # Identify the sorted half
        # 1. Left side is sorted
        if nums[low] <= nums[mid]:
            # Check if target is in the left sorted range
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1
        
        # 2. Right side is sorted
        else:
            # Check if target is in the right sorted range
            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1
                
    return -1
```

---

## Dry Run (Smart Example)

**Input:** `nums = [4, 5, 6, 7, 0, 1, 2]`, `target = 0`

| Step | low | high | mid | nums[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 7 | Left side [4,5,6,7] sorted. 0 is NOT in [4,7]. Move `low = 4`. |
| 2 | 4 | 6 | 5 | 1 | Right side [1,2] sorted. 0 is NOT in [1,2]. Move `high = 4`. |
| 3 | 4 | 4 | 4 | 0 | `nums[mid] == 0`. Target found at index 4. |

---

## Edge Cases

- **Single Element:** `nums = [1], target = 0` (Handled by `low <= high`).
- **Array Not Rotated:** Standard binary search behavior still applies.
- **Target at Pivot:** `nums = [4, 5, 1, 2, 3], target = 1` (Mid hits pivot).
- **Two Elements:** `nums = [3, 1], target = 1` (Pivot handling).

---

## Mistakes

- **Incorrect Sorted Check:** Trying to check if the target is in a half before verifying if that half is sorted.
- **Equality Signs:** Forgetting `nums[low] <= nums[mid]`. Without the `=`, the logic fails on two-element arrays.
- **Range Logic:** Missing the boundary check `nums[low] <= target < nums[mid]`.
- **User Mistake:** Failing the pattern to check the sorted part; always verify `nums[low] <= nums[mid]` first.

---

## Complexity

Time: O(log N) → Standard binary search reduces search space by half each iteration.  
Space: O(1) → Iterative approach uses only a few pointers.

---

## Tags and Properties
- #dsa #important #revisit #search #binarysearch
- [[Binary Search]] [[Arrays]] [[Divide and Conquer]]
- Revision Date: 2026-04-01
- Related: [[Search in Rotated Sorted Array II]], [[Find Minimum in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-03)
- [ ] Day 7 Revision (2026-04-08)
- [ ] Day 15 Revision (2026-04-16)
- [ ] Day 30 Revision (2026-05-01)
