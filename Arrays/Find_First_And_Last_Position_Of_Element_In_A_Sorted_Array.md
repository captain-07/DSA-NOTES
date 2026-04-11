---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

I will generate the high-signal markdown note for "Find First and Last Position of Element in a Sorted Array" following your strict structural requirements and Obsidian-friendly formatting.

# Find First And Last Position Of Element In A Sorted Array

---

## Pattern

Binary Search (Modified for Boundaries)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- In a sorted array, the first and last positions are the **leftmost** and **rightmost** boundaries of the target.
- Standard Binary Search finds *any* occurrence; to find boundaries, continue searching in the left half for the "first" and the right half for the "last" even after finding the target.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Run Binary Search twice: one to find `bisect_left` (first occurrence) and one for `bisect_right - 1` (last occurrence).

---

## Approach

### Brute Force
- Linear scan from left to right to find the first index, then from right to left for the last index.
- Time: O(N)

### Better
- Use a single Binary Search to find any instance of the target, then expand outwards to find boundaries.
- Time: O(N) in worst case (all elements are the same).

### Optimal
- Two independent Binary Searches.
- **First Search:** If `nums[mid] >= target`, move `right = mid - 1` to find the leftmost index.
- **Second Search:** If `nums[mid] <= target`, move `left = mid + 1` to find the rightmost index.
- Only update the result index when `nums[mid] == target`.

---

## Code (Python)

```python
class Solution:
    def searchRange(self, nums: list[int], target: int) -> list[int]:
        def find_bound(is_first: bool) -> int:
            left, right = 0, len(nums) - 1
            bound = -1
            
            while left <= right:
                mid = (left + right) // 2
                
                if nums[mid] == target:
                    bound = mid
                    if is_first:
                        right = mid - 1 # Keep looking left
                    else:
                        left = mid + 1  # Keep looking right
                elif nums[mid] < target:
                    left = mid + 1
                else:
                    right = mid - 1
            return bound

        return [find_bound(True), find_bound(False)]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [5, 7, 7, 8, 8, 10]`, `target = 8`

| Step | Search Type | Variables (L, R, M) | nums[M] | Action | Bound |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | First (Left) | L=0, R=5, M=2 | 7 | 7 < 8, L = M + 1 | -1 |
| 2 | First (Left) | L=3, R=5, M=4 | 8 | 8 == 8, R = M - 1 | 4 |
| 3 | First (Left) | L=3, R=3, M=3 | 8 | 8 == 8, R = M - 1 | 3 |
| 4 | Second (Right)| L=0, R=5, M=2 | 7 | 7 < 8, L = M + 1 | -1 |
| 5 | Second (Right)| L=3, R=5, M=4 | 8 | 8 == 8, L = M + 1 | 4 |
| 6 | Second (Right)| L=5, R=5, M=5 | 10| 10 > 8, R = M - 1 | 4 |

---

## Edge Cases

- **Empty Array:** `nums = []` → Return `[-1, -1]`.
- **Target Not Present:** `nums = [1, 2, 4]`, `target = 3` → Return `[-1, -1]`.
- **Target is All Elements:** `nums = [5, 5, 5]`, `target = 5` → Return `[0, 2]`.
- **Single Element (Match):** `nums = [1]`, `target = 1` → Return `[0, 0]`.
- **Single Element (No Match):** `nums = [1]`, `target = 2` → Return `[-1, -1]`.

---

## Mistakes

- Using standard `binary_search` and then expanding linearly (degrades to O(N)).
- Forgetting to handle the "not found" case correctly.
- Off-by-one errors in `mid` calculation or boundary updates.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Two binary search passes, each taking logarithmic time.  
Space: O(1) → Constant space used for pointers and boundaries.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #leetcode34
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-11
  - **Problem Link:** [LeetCode - Find First and Last Position of Element in a Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-a-sorted-array/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Bloomberg #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]], #rangequery [[Range Query]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
