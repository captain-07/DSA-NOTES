---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Binary Search

---

## Pattern

Divide and Conquer (Search Space Reduction)

---
## Difficulty

Easy  
#easy

---
## ⚡ Key Idea (Core Insight)

Exploit the **sorted** property of an array to eliminate half of the search space in each step. By comparing the target with the middle element, you determine if the target lies in the left or right half.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Maintain `low` and `high` pointers. While `low <= high`, calculate `mid = low + (high - low) // 2` and shrink the range based on `nums[mid]` vs `target`.

---
## Approach

### Brute Force
- Linear Search: Iterate through every element to find the target.
- Time: O(N)
- Space: O(1)

### Optimal
- **Iterative Binary Search**:
  1. Initialize `low = 0`, `high = len(nums) - 1`.
  2. Loop while `low <= high`.
  3. Calculate `mid`.
  4. If `nums[mid] == target`, return `mid`.
  5. If `nums[mid] < target`, move `low = mid + 1`.
  6. Else, move `high = mid - 1`.
  7. Return -1 if not found.

---
## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        low, high = 0, len(nums) - 1
        
        while low <= high:
            # Prevent potential integer overflow (though not an issue in Python)
            mid = low + (high - low) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                low = mid + 1
            else:
                high = mid - 1
                
        return -1
```

---
## Dry Run (Smart Example)

**Input:** `nums = [-1, 0, 3, 5, 9, 12]`, `target = 9`

| Step | low | high | mid | nums[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 3 | `3 < 9`, so `low = mid + 1 = 3`. |
| 2 | 3 | 5 | 4 | 9 | `9 == 9`, Target found! Return index 4. |

---
## Edge Cases

- **Empty Array:** `nums = []`. Loop won't execute, returns -1.
- **Single Element:** `nums = [5], target = 5`. `low=0, high=0, mid=0`. Found.
- **Target Not Present:** `nums = [1, 3], target = 2`. `low` will eventually exceed `high`.
- **Target at Boundaries:** Target is at index `0` or `len-1`.

---
## Mistakes

- **Infinite Loop:** Using `while low < high` instead of `low <= high` (misses the last element).
- **Integer Overflow:** Using `(low + high) // 2` in languages with fixed-size integers (use `low + (high - low) // 2`).
- **Incorrect Updates:** Doing `low = mid` or `high = mid` instead of `mid + 1` / `mid - 1` can cause infinite loops.
- **Unsorted Input:** Binary search fails if the array is not sorted.
- **User Mistake:** No specific note provided.

---
## Complexity

Time: O(log N) → Search space is halved in every iteration.  
Space: O(1) → Iterative approach uses only a few variables.

---
## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy

---
## Tags and Properties

- #dsa #important #revisit #basics #searching
- [[Binary Search]] [[Arrays]] [[Divide and Conquer]]
- **Revision Date:** 2026-04-11
- **Problem Link:** [LeetCode - Binary Search](https://leetcode.com/problems/binary-search/)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Apple #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #searching [[Searching]], #divideandconquer [[Divide and Conquer]]

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
