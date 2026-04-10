---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Binary Search

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #Apple #Bloomberg #Netflix #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #searching [[Searching]], #array [[Array]], #divide-and-conquer [[Divide and Conquer]]

## Pattern

Binary Search (Divide and Conquer / Half-Interval Search)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

- Exploits the sorted property of an array to reduce the search space by half in each step. 
- By comparing the target with the middle element, we can eliminate the half where the target cannot possibly exist.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Sorted Array? -> `mid = left + (right - left) // 2`. If `arr[mid] < target`, `left = mid + 1`, else `right = mid - 1`.

---

## Approach

### Brute Force
- Linear search through the entire array.
- Time: $O(n)$, Space: $O(1)$.

### Optimal
- Initialize two pointers: `left = 0` and `right = len(nums) - 1`.
- While `left <= right`:
    - Calculate `mid` to avoid overflow.
    - If `nums[mid] == target`, return `mid`.
    - If `nums[mid] < target`, discard the left half (`left = mid + 1`).
    - If `nums[mid] > target`, discard the right half (`right = mid - 1`).
- Return -1 if not found.

---

## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        if not nums:
            return -1
            
        left, right = 0, len(nums) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
                
        return -1
```

---

## Dry Run (Smart Example)

Input: `nums = [-1, 0, 3, 5, 9, 12], target = 9`

| Step | Left | Right | Mid | `nums[mid]` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 3 | $3 < 9$, so `left = 2 + 1 = 3` |
| 2 | 3 | 5 | 4 | 9 | $9 == 9$, Target found at index 4 |

---

## Edge Cases

- **Empty Array:** Should return -1 immediately.
- **Single Element:** Check if `nums[0]` is the target.
- **Target at Boundaries:** Target is the first or last element.
- **Target Not Present:** `left` will eventually exceed `right`.
- **Large Arrays:** Ensure `mid` calculation doesn't overflow (though Python handles large integers, this is a standard interview point).

---

## Mistakes

- **CRITICAL:** Forgot to handle empty array (`if not nums: return -1`).
- **Off-by-one:** Using `while left < right` instead of `while left <= right`.
- **Mid Overflow:** Using `(left + right) // 2` instead of `left + (right - left) // 2`.
- **Incorrect Update:** Forgetting the `+1` or `-1` when updating `left` or `right`.

---

## Complexity

Time: $O(\log n)$ → The search space is halved in every iteration.  
Space: $O(1)$ → Only a constant amount of extra space is used for pointers.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First and Last Position of Element](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
- #dsa #important #revisit #blind75
- #binary-search [[Binary Search]], #searching [[Searching]], #sorting [[Sorting]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [LeetCode Binary Search](https://leetcode.com/problems/binary-search/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
