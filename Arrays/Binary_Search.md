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
  - #Google #Amazon #Microsoft #Meta #Apple #Uber #Netflix

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #searching [[Searching]], #divideandconquer [[Divide and Conquer]]

## Pattern

- Decrease and Conquer (Halving the search space)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Binary Search leverages the **sorted** property of an array to eliminate half of the remaining elements in each step. By comparing the target value to the middle element, we decide whether to search the left or right half.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Calculate `mid`, if `target > nums[mid]` move `left` to `mid + 1`, else move `right` to `mid - 1`.

---

## Approach

### Brute Force
- Perform a Linear Search by iterating through every element until the target is found.
- **Time Complexity:** O(N)

### Optimal (Iterative)
1. Initialize two pointers: `left = 0` and `right = n - 1`.
2. While `left <= right`:
    - Calculate `mid = left + (right - left) // 2` (prevents overflow).
    - If `nums[mid] == target`, return `mid`.
    - If `nums[mid] < target`, discard the left half: `left = mid + 1`.
    - If `nums[mid] > target`, discard the right half: `right = mid - 1`.
3. If the loop ends, the target is not in the array; return -1.

---

## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        
        while left <= right:
            # Optimal mid calculation to prevent potential overflow
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
| 1 | L=0, R=5, M=2 | `nums[2] = 3`. Since `3 < 9`, move `L` to `M + 1` (3). |
| 2 | L=3, R=5, M=4 | `nums[4] = 9`. Since `9 == 9`, target found. |
| 3 | - | Return index 4. |

---

## Edge Cases

- **Target not present:** The pointers cross (`left > right`), return -1.
- **Single element array:** Correctly identifies if the single element matches target.
- **Target at boundaries:** Target is the first (`index 0`) or last (`index n-1`) element.
- **Empty array:** `left` (0) is not `<= right` (-1), loop never starts, returns -1.

---

## Mistakes

- **Overflow:** Using `(left + right) // 2` instead of `left + (right - left) // 2` in languages with fixed-size integers.
- **Infinite Loop:** Forgetting to update pointers as `mid + 1` or `mid - 1`, causing the window to never shrink.
- **Condition:** Using `while left < right` instead of `while left <= right`, missing the last possible element.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → The search space is halved in every iteration.  
Space: O(1) → Only a constant amount of extra space is used for pointers.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #searching #binarysearch #arrays
  - [[Binary Search]] [[Arrays]] [[Searching]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [Binary Search - LeetCode](https://leetcode.com/problems/binary-search/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
