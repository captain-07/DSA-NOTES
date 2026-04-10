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
  - #Amazon #Google #Microsoft #Meta #Apple #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #sorting [[Sorting]], #divideandconquer [[Divide and Conquer]]

## Pattern

- Binary Search (Decrease and Conquer)
- Two Pointers (Left and Right boundaries)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

In a **sorted** search space, compare the middle element with the target. Based on the comparison, discard exactly half of the remaining elements in each step, reducing the search space logarithmically.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Maintain `left` and `right` pointers. While `left <= right`, check `mid`. If `target > nums[mid]`, search right (`left = mid + 1`); otherwise, search left (`right = mid - 1`).

---

## Approach

### Brute Force
- Linear Search: Iterate through every element in the array until the target is found or the end is reached.
- **Time Complexity:** O(N)

### Optimal
- **Initialization:** Set `left = 0` and `right = len(nums) - 1`.
- **Iteration:** While `left <= right`:
    - Calculate `mid = left + (right - left) // 2` (prevents overflow in other languages).
    - If `nums[mid] == target`, return `mid`.
    - If `nums[mid] < target`, move `left = mid + 1`.
    - If `nums[mid] > target`, move `right = mid - 1`.
- **Termination:** If the loop ends without finding the target, return -1.
- **Time Complexity:** O(log N)

---

## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        
        while left <= right:
            # Standard mid calculation
            mid = left + (right - left) // 2
            
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                # Target is in the right half
                left = mid + 1
            else:
                # Target is in the left half
                right = mid - 1
                
        return -1
```

---

## Dry Run (Smart Example)

**Input:** `nums = [-1, 0, 3, 5, 9, 12]`, `target = 9`

| Step | Variables (L, R, M) | Explanation |
| :--- | :--- | :--- |
| 1 | L=0, R=5, M=2 | `nums[2] = 3`. Since `3 < 9`, target is on the right. Move `L = 2 + 1 = 3`. |
| 2 | L=3, R=5, M=4 | `nums[4] = 9`. `9 == 9`. Target found! |
| 3 | - | Return index `4`. |

---

## Edge Cases

- **Empty Array:** `nums = []`, should return -1 immediately.
- **Single Element:** `nums = [5]`, `target = 5`. Loop runs once, returns 0.
- **Target at Boundaries:** Target is the first or last element.
- **Target Not Present:** `left` becomes greater than `right`, loop terminates, returns -1.
- **Large Arrays:** Ensure `mid` calculation doesn't overflow (handled natively in Python).

---

## Mistakes

- **Incorrect Loop Condition:** Using `while left < right` instead of `while left <= right` (misses the last element).
- **Boundary Updates:** Forgetting the `+ 1` or `- 1` when updating `left` or `right`, leading to infinite loops.
- **Unsorted Input:** Attempting Binary Search on an unsorted array without sorting it first.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → The search space is halved in every iteration.  
Space: O(1) → Only a constant amount of extra space is used for pointers.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #searching 
  - #algorithms [[Binary Search]] [[Searching Algorithms]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode 704 - Binary Search](https://leetcode.com/problems/binary-search/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
