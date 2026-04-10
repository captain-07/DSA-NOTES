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
  - #Amazon #Google #Facebook #Microsoft #LinkedIn #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

---
## Pattern

Modified Binary Search (Search for boundaries)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

- Since the array is sorted, we must use **Binary Search** to achieve $O(\log n)$.
- A single binary search finds *an* occurrence; two modified searches are needed to find the **first** and **last** occurrences by continuing the search even after the target is found.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- To find the **left bound**: If `nums[mid] == target`, keep searching left (`high = mid - 1`).
- To find the **right bound**: If `nums[mid] == target`, keep searching right (`low = mid + 1`).

---

## Approach

### Brute Force
- Linear scan from left to find the first index, then linear scan from right to find the last index.
- Time: $O(n)$

### Optimal
- Run Binary Search twice.
- **First Pass:** Find the leftmost index where `nums[i] == target`.
- **Second Pass:** Find the rightmost index where `nums[i] == target`.
- If the first pass doesn't find the target, return `[-1, -1]` immediately.
- Time: $O(\log n)$

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
                        high = mid - 1 # Look left for first position
                    else:
                        low = mid + 1  # Look right for last position
                elif nums[mid] < target:
                    low = mid + 1
                else:
                    high = mid - 1
            return bound

        return [findBound(True), findBound(False)]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [5, 7, 7, 8, 8, 10], target = 8`

| Step | Search Type | Low | High | Mid | `nums[mid]` | Action | Bound |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | First Bound | 0 | 5 | 2 | 7 | `low = mid + 1` | -1 |
| 2 | First Bound | 3 | 5 | 4 | 8 | `bound = 4`, `high = 3` | 4 |
| 3 | First Bound | 3 | 3 | 3 | 8 | `bound = 3`, `high = 2` | 3 |
| 4 | Last Bound | 0 | 5 | 2 | 7 | `low = mid + 1` | -1 |
| 5 | Last Bound | 3 | 5 | 4 | 8 | `bound = 4`, `low = 5` | 4 |
| 6 | Last Bound | 5 | 5 | 5 | 10 | `high = 4` | 4 |

**Result:** `[3, 4]`

---

## Edge Cases

- **Empty Array:** `nums = []` → Returns `[-1, -1]`.
- **Target Not Present:** `target = 6` in `[5, 7, 8]` → Returns `[-1, -1]`.
- **Single Element:** `nums = [8], target = 8` → Returns `[0, 0]`.
- **All Elements are Target:** `nums = [8, 8, 8], target = 8` → Returns `[0, 2]`.

---

## Mistakes

- **Off-by-one errors:** Forgetting to update `low` or `high` correctly in the modified binary search.
- **Early Exit:** Stopping search immediately after finding the target once.
- **Empty Array:** Not checking if `nums` is empty before processing.
- **User mistake:** No specific note provided.

---

## Complexity

Time: $O(\log n)$ → We perform two independent binary searches.  
Space: $O(1)$ → Only a few pointers are used regardless of input size.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #arrays
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
