---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

I will generate the high-signal DSA note for "Find First And Last Position Of Element In A Sorted Array" and save it to your Obsidian vault as mandated.

# Find First And Last Position Of Element In A Sorted Array

---

## Pattern

Modified Binary Search (Boundary Finding)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The array is sorted, but contains duplicates. Standard binary search finds *any* occurrence. To find boundaries, when `nums[mid] == target`, **continue searching** in the left half for the start index and in the right half for the end index, storing the "last seen" valid index.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Run Binary Search twice. Use a flag `findFirst`:
- If `findFirst` and `nums[mid] == target`, set `ans = mid` and `high = mid - 1`.
- If `!findFirst` and `nums[mid] == target`, set `ans = mid` and `low = mid + 1`.

---

## Approach

### Brute Force
- Linear scan from left to find first, then from right to find last.
- Time: $O(n)$
- Space: $O(1)$

### Better
- Binary search to find any index, then expand left and right linearly.
- Time: $O(n)$ worst case (e.g., all elements are the target).
- Space: $O(1)$

### Optimal
- Two independent Binary Searches to find the lower and upper bounds.
- Time: $O(\log n)$
- Space: $O(1)$

---

## Code (Python)

```python
class Solution:
    def searchRange(self, nums: list[int], target: int) -> list[int]:
        def findBound(isFirst: bool) -> int:
            low, high = 0, len(nums) - 1
            ans = -1
            
            while low <= high:
                mid = (low + high) // 2
                
                if nums[mid] == target:
                    ans = mid
                    # If looking for first, narrow search to the left
                    if isFirst:
                        high = mid - 1
                    # If looking for last, narrow search to the right
                    else:
                        low = mid + 1
                elif nums[mid] < target:
                    low = mid + 1
                else:
                    high = mid - 1
            return ans
        
        return [findBound(True), findBound(False)]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [5, 7, 7, 8, 8, 10], target = 8`

| Step | `isFirst` | `low`, `high`, `mid` | `nums[mid]` | `ans` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | True | 0, 5, 2 | 7 | -1 | `7 < 8`, move `low` to 3 |
| 2 | True | 3, 5, 4 | 8 | 4 | Found 8, move `high` to 3 to find earlier |
| 3 | True | 3, 3, 3 | 8 | 3 | Found 8 at index 3, move `high` to 2 |
| 4 | False | 0, 5, 2 | 7 | -1 | `7 < 8`, move `low` to 3 |
| 5 | False | 3, 5, 4 | 8 | 4 | Found 8, move `low` to 5 to find later |
| 6 | False | 5, 5, 5 | 10 | 4 | `10 > 8`, move `high` to 4. Loop ends. |

---

## Edge Cases

- **Empty Array:** `nums = []` → Return `[-1, -1]`.
- **Target Not Present:** `nums = [1, 2, 4], target = 3` → Return `[-1, -1]`.
- **Single Element (Match):** `nums = [5], target = 5` → Return `[0, 0]`.
- **All Elements are Target:** `nums = [8, 8, 8], target = 8` → Return `[0, 2]`.

---

## Mistakes

- Using standard `bisect_left` or `bisect_right` without checking if the returned index actually matches the target.
- Returning immediately after finding one instance of the target.
- Incorrectly handling the case where `nums` is empty.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(\log n)$ → Two binary searches take $2 \times O(\log n)$.  
Space: $O(1)$ → Only a few pointers used.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #array
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-11
  - **Problem Link:** [LeetCode 34 - Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-a-sorted-array/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Facebook #Microsoft #LinkedIn #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]]

---
### 🔄 Revision Checklist
- [x] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
