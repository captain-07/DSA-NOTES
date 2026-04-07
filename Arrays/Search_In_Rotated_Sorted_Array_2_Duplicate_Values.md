---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Search In Rotated Sorted Array 2 [Duplicate Values]

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #LinkedIn #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Array]]
  - #duplicates [[Handling Duplicates]]

## Pattern

Modified Binary Search + Linear Shrink  

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- In a rotated sorted array, at least one half (left or right) is always sorted.
- **The Duplicate Problem:** If `nums[left] == nums[mid] == nums[right]`, we cannot determine which half is sorted.
- **The Unlock:** In the ambiguous case, simply shrink the search space by incrementing `left` and decrementing `right` until the ambiguity is resolved.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Standard Rotated Binary Search, but add `if nums[L] == nums[M] == nums[R]: L++; R--` to handle duplicates before checking sorted halves.

---

## Approach

### Brute Force
- Linear search through the entire array.
- **Time:** O(N)

### Better
- Sort the array first (if not already "sorted-rotated") and use standard Binary Search.
- **Time:** O(N log N) - Inferior to brute force for this specific problem.

### Optimal (Modified Binary Search)
1. Initialize `left = 0`, `right = len(nums) - 1`.
2. While `left <= right`:
   - Calculate `mid`.
   - If `nums[mid] == target`, return `True`.
   - **Critical Step:** If `nums[left] == nums[mid] == nums[right]`, increment `left` and decrement `right`.
   - Otherwise, identify the sorted half:
     - If `nums[left] <= nums[mid]` (Left side is sorted): Check if target is within `[nums[left], nums[mid])`.
     - Else (Right side is sorted): Check if target is within `(nums[mid], nums[right]]`.
3. Return `False` if not found.

---

## Code (Python)

```python
def search(nums: list[int], target: int) -> bool:
    low, high = 0, len(nums) - 1
    
    while low <= high:
        mid = (low + high) // 2
        
        if nums[mid] == target:
            return True
            
        # Ambiguous case due to duplicates
        if nums[low] == nums[mid] == nums[high]:
            low += 1
            high -= 1
            continue
            
        # Left side is sorted
        if nums[low] <= nums[mid]:
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1
        # Right side is sorted
        else:
            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1
                
    return False
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 0, 1, 1, 1]`, `target = 0`

| Step | L, M, R | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | 0, 2, 4 | `nums[0]=1, nums[2]=1, nums[4]=1` | `nums[L]==nums[M]==nums[R]`. Shrink: `L=1, R=3`. |
| 2 | 1, 2, 3 | `nums[1]=0, nums[2]=1, nums[3]=1` | `nums[M]=1`. Left half `[1, 2]` is sorted (`0 <= 1`). |
| 3 | 1, 1, 1 | `nums[1]=0` | `nums[1] == target`. Return `True`. |

---

## Edge Cases

- `[1]`: Single element matching/not matching target.
- `[1, 1, 1, 1]`: All elements identical to each other but not the target.
- `[3, 1]`: Minimum rotation, two elements.
- Target is the pivot element itself.

---

## Mistakes

- **Incorrect Duplicate Handling:** Forgetting to check `nums[low] == nums[mid] == nums[high]` leads to incorrect "sorted half" logic.
- **Strict Inequalities:** Using `<` instead of `<=` when checking if target is within the sorted range.
- **User Mistake:** None.

---

## Complexity

- **Time:** Average O(log N). Worst case O(N) when all elements are duplicates (e.g., `[1, 1, 1]` searching for `0`).
- **Space:** O(1) as we only use pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #interview-prep
  - [[Binary Search]] [[Array]] [[Two Pointers]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode 81 - Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
