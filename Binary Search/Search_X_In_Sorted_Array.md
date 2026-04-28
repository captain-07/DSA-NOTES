---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Search X In Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Array]]
  - #divideandconquer [[Divide and Conquer]]

## Pattern

Binary Search (Decrease and Conquer)

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

The array is **sorted**. Instead of checking every element, compare the target `X` with the middle element. Since the data is ordered, you can discard exactly half of the remaining search space in every step ($O(\log N)$).

---

## ⚡ Quick Recall (VERY IMPORTANT)

`low, high = 0, len-1`. While `low <= high`, calculate `mid`. If `nums[mid] == X` return index. If `nums[mid] < X`, move `low` up; else move `high` down.

---

## Approach

### Brute Force
- Linear Search: Iterate from index `0` to `N-1`.
- Time Complexity: $O(N)$

### Optimal (Binary Search)
1. Initialize `low = 0` and `high = n - 1`.
2. While `low <= high`:
    - Calculate `mid = low + (high - low) // 2` (prevents overflow).
    - If `arr[mid] == X`, return `mid`.
    - If `arr[mid] < X`, discard left half: `low = mid + 1`.
    - If `arr[mid] > X`, discard right half: `high = mid - 1`.
3. If loop ends, `X` is not present. Return `-1`.

---

## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        low = 0
        high = len(nums) - 1
        
        while low <= high:
            # Standard mid calculation to avoid potential overflow
            mid = low + (high - low) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                # Target is in the right half
                low = mid + 1
            else:
                # Target is in the left half
                high = mid - 1
                
        return -1
```

---

## Dry Run (Smart Example)

**Input:** `nums = [-1, 0, 3, 5, 9, 12]`, `target = 9`

| Step | low | high | mid | nums[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 3 | `3 < 9`, discard left: `low = 3` |
| 2 | 3 | 5 | 4 | 9 | `9 == 9`, Found! Return index `4` |

---

## Edge Cases

- **Empty Array:** `nums = []`. Loop won't start; returns `-1`.
- **Single Element:** `nums = [5]`, `target = 5`. Returns `0` (low=high=mid).
- **Target at Boundaries:** `X` is the first or last element.
- **Target Missing:** `X` is smaller than min or larger than max.
- **Duplicates:** Standard BS returns *any* index of `X`.

---

## Mistakes

- **Termination Condition:** Using `low < high` instead of `low <= high` (misses the last element).
- **Update Logic:** Forgetting `+ 1` or `- 1` when updating `low`/`high`, leading to infinite loops.
- **Mid Overflow:** In some languages, `(low + high) // 2` can overflow; use `low + (high - low) // 2`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: $O(\log N)$ → Search space is halved in each iteration.  
Space: $O(1)$ → Iterative approach uses constant extra space.

---

## Similar Problems

- [Binary Search](https://leetcode.com/problems/binary-search/) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch 
  - [[Binary Search]] [[Searching Algorithms]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode 704 - Binary Search](https://leetcode.com/problems/binary-search/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
