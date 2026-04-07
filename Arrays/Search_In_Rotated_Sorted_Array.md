---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Search In Rotated Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #searching [[Searching]]

## Pattern

Modified Binary Search (Sorted Half Identification)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Even in a rotated array, **at least one half** (left or right) relative to the `mid` pointer is always strictly sorted. By identifying which half is sorted, we can determine if the `target` lies within its range using simple boundary checks, effectively halving the search space in each step.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Find the sorted half first (`nums[low] <= nums[mid]`). If the target is within the bounds of that sorted half, search there; otherwise, search the other half.

---

## Approach

### Brute Force
- Linear search through the array from index 0 to $n-1$.
- Time Complexity: O(n)
- Space Complexity: O(1)

### Optimal
- **Modified Binary Search:**
  1. Initialize `low = 0`, `high = n - 1`.
  2. While `low <= high`, find `mid`.
  3. If `nums[mid] == target`, return `mid`.
  4. **Check Left Half (`nums[low] <= nums[mid]`):**
     - If `nums[low] <= target < nums[mid]`, search left (`high = mid - 1`).
     - Else, search right (`low = mid + 1`).
  5. **Otherwise, Right Half is sorted:**
     - If `nums[mid] < target <= nums[high]`, search right (`low = mid + 1`).
     - Else, search left (`high = mid - 1`).

---

## Code (Python)

```python
def search(nums: list[int], target: int) -> int:
    low, high = 0, len(nums) - 1
    
    while low <= high:
        mid = (low + high) // 2
        
        if nums[mid] == target:
            return mid
            
        # Case 1: Left side is sorted
        if nums[low] <= nums[mid]:
            # Target lies within the sorted left range
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1
        
        # Case 2: Right side is sorted
        else:
            # Target lies within the sorted right range
            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1
                
    return -1
```

---

## Dry Run (Smart Example)

Input: `nums = [4, 5, 6, 7, 0, 1, 2]`, `target = 0`

| Step | Variables (low, mid, high) | Explanation |
| :--- | :--- | :--- |
| 1 | `L=0, M=3, H=6` | `nums[M]=7`. Left half `[4,7]` is sorted. `0` is not in `[4, 7]`. Set `L = M + 1 (4)`. |
| 2 | `L=4, M=5, H=6` | `nums[M]=1`. Right half `[1,2]` is sorted. `0` is not in `[1, 2]`. Set `H = M - 1 (4)`. |
| 3 | `L=4, M=4, H=4` | `nums[M]=0`. `0 == target`. Return index `4`. |

---

## Edge Cases

- **Empty Array:** Returns -1 immediately.
- **Single Element:** Correctly handles if the element is or isn't the target.
- **No Rotation:** Standard binary search behavior naturally handles a fully sorted array.
- **Target at Pivot:** Correctly identified when `mid` lands on either side of the rotation point.

---

## Mistakes

- **User Warning:** Failing the pattern to check the sorted part; always verify `nums[low] <= nums[mid]` first.
- Using `target <= nums[mid]` instead of `target < nums[mid]` when the target is already checked at `mid`.
- Forgetting to handle the "Right side is sorted" logic as a fallback to the left-side check.

---

## Complexity

Time: O(log n) → Search space is halved in every iteration.  
Space: O(1) → Iterative solution uses only constant extra pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Search in a Sorted Array of Unknown Size](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #arrays #interview-kit
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
