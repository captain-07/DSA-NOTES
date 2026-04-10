---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

I will start by reading `config.json` and `dsa/router.py` to ensure the note is saved in the correct vault path and category as per the project mandates.
I will now generate the markdown note for the problem "Search In Rotated Sorted Array 2 [Duplicate Values]" and save it to the Obsidian vault as per the project mandates.

# Search In Rotated Sorted Array 2 [Duplicate Values]

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #LinkedIn #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]], #duplicates [[Duplicate Handling]]

## Pattern

Binary Search on Rotated Array (with Duplicate Handling)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

- Standard binary search logic fails when `nums[left] == nums[mid] == nums[right]` because we cannot determine which half is sorted.
- **The Fix:** If the triplet is equal, simply shrink the search space by `low += 1` and `high -= 1` until the ambiguity is resolved. This "shaves off" the duplicates that prevent us from identifying the sorted half.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- If `nums[low] == nums[mid] == nums[high]`, just `low++, high--`. Otherwise, proceed with standard rotated binary search logic to identify the sorted half.

---

## Approach

### Brute Force
- Linear search through the array to find the target.
- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$

### Optimal
- **Modified Binary Search**:
  1. Calculate `mid`.
  2. If `nums[mid] == target`, return `True`.
  3. **Handle Duplicates**: If `nums[low] == nums[mid] == nums[high]`, increment `low` and decrement `high`. `continue` to next iteration.
  4. **Identify Sorted Half**: 
     - If `nums[low] <= nums[mid]`, the left side is sorted.
     - Else, the right side is sorted.
  5. **Prune Range**: If the target lies within the range of the sorted half, search there; otherwise, search the other half.

---

## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> bool:
        low, high = 0, len(nums) - 1
        
        while low <= high:
            mid = low + (high - low) // 2
            
            if nums[mid] == target:
                return True
            
            # Handle duplicates: the critical part for SRSA 2
            if nums[low] == nums[mid] == nums[high]:
                low += 1
                high -= 1
                continue
            
            # Left half is sorted
            if nums[low] <= nums[mid]:
                if nums[low] <= target < nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            # Right half is sorted
            else:
                if nums[mid] < target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1
                    
        return False
```

---

## Dry Run (Smart Example)

**Input**: `nums = [1,0,1,1,1]`, `target = 0`

| Step | low | high | mid | nums[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 4 | 2 | 1 | `nums[0]==nums[2]==nums[4]`. Ambiguous. `low=1`, `high=3`. |
| 2 | 1 | 3 | 2 | 1 | `nums[low] (0) <= nums[mid] (1)`. Left sorted. Target 0 in range `[0, 1]`. `high=1`. |
| 3 | 1 | 1 | 1 | 0 | `nums[1] == target`. Return **True**. |

---

## Edge Cases

- **Single element array**: `[1], target=0` -> Correctly returns `False`.
- **All elements identical**: `[1,1,1], target=1` -> Returns `True` instantly or after shrinking.
- **Pivot at extreme ends**: `[1,2,3,4,0]` or `[4,0,1,2,3]` -> Handled by sorted-side logic.
- **Target at pivot**: `[2,5,6,0,0,1,2], target=0` -> Found immediately or after division.

---

## Mistakes

- **Incorrect Complexity**: Do not claim strictly $O(\log n)$. In the worst case (e.g., `[1,1,1,1,1]`), it degrades to $O(n)$.
- **Missing the Duplicate Check**: Forgetting `nums[low] == nums[mid] == nums[high]` will cause the algorithm to choose the wrong half or fail.
- **User Mistake**: None.

---

## Complexity

Time: $O(\log n)$ average, $O(n)$ worst case (all duplicates).  
Space: $O(1)$ iterative approach uses constant space.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) - Hard
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Arrays]]
  - Revision Date: 2026-04-10
  - **Problem Link:** [Search in Rotated Sorted Array II - LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
