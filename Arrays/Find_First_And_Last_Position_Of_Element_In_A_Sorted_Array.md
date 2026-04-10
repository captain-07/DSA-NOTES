---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Find First And Last Position Of Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Facebook #Google #Amazon #Microsoft #LinkedIn #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]]

## Pattern

Modified Binary Search (Find boundaries)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The array is sorted, but contains duplicates. A standard Binary Search finds *any* occurrence. To find boundaries, when `nums[mid] == target`, don't stop; instead, record the index and continue searching in the left half for the "First" position or the right half for the "Last" position.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Run Binary Search twice. If `nums[mid] == target`, update `ans` and move `high = mid - 1` (for first) or `low = mid + 1` (for last).

---

## Approach

### Brute Force
- Linear scan the entire array to find the first and last occurrence.
- Time: O(N)

### Better
- Binary search to find any occurrence, then expand linearly left and right to find boundaries.
- Time: O(log N) average, but O(N) worst case (e.g., all elements are the same).

### Optimal
- Two independent Binary Searches: one specifically for the leftmost boundary and one for the rightmost.
- Time: O(log N) guaranteed.

---

## Code (Python)

```python
class Solution:
    def searchRange(self, nums: list[int], target: int) -> list[int]:
        def findBound(isFirst: bool) -> int:
            low, high = 0, len(nums) - 1
            bound = -1
            
            while low <= high:
                mid = (low + high) // 2
                
                if nums[mid] == target:
                    bound = mid
                    if isFirst:
                        high = mid - 1 # Look left
                    else:
                        low = mid + 1  # Look right
                elif nums[mid] < target:
                    low = mid + 1
                else:
                    high = mid - 1
            return bound

        return [findBound(True), findBound(False)]
```

---

## Dry Run (Smart Example)

Input: `nums = [5, 7, 7, 8, 8, 10]`, `target = 8`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 (First) | `low=0, high=5, mid=2 (val=7)` | `7 < 8`, move `low = 3`. |
| 2 (First) | `low=3, high=5, mid=4 (val=8)` | `8 == 8`, `bound = 4`, move `high = 3`. |
| 3 (First) | `low=3, high=3, mid=3 (val=8)` | `8 == 8`, `bound = 3`, move `high = 2`. Exit. **First = 3**. |
| 4 (Last) | `low=0, high=5, mid=2 (val=7)` | `7 < 8`, move `low = 3`. |
| 5 (Last) | `low=3, high=5, mid=4 (val=8)` | `8 == 8`, `bound = 4`, move `low = 5`. |
| 6 (Last) | `low=5, high=5, mid=5 (val=10)`| `10 > 8`, move `high = 4`. Exit. **Last = 4**. |

---

## Edge Cases

- **Target not in array:** Both searches return -1.
- **Empty array:** Loops never run, returns `[-1, -1]`.
- **All elements are target:** First search converges to index 0, last to `len-1`.
- **Single element array:** Correctly handles `[target]` or `[non-target]`.

---

## Mistakes

- Using standard `bisect_left` / `bisect_right` without checking if the target actually exists at the returned index.
- Forgetting to update `bound` when `nums[mid] == target`.
- Not handling the empty array case explicitly if the template requires it.
- **User mistake:** None.

---

## Complexity

Time: O(log N) → Two independent binary searches performed on the array.  
Space: O(1) → Only a few pointers and variables used.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Count Occurrences in Sorted Array](https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #sortedarray #rangefinding
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Find First and Last Position of Element in a Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-a-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
