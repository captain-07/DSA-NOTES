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

<<<<<<< HEAD
## Pattern

Divide and Conquer (Search Space Reduction)
=======
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
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Difficulty

Easy  
#easy

---
## ⚡ Key Idea (Core Insight)

<<<<<<< HEAD
Exploit the **sorted** property of an array to eliminate half of the search space in each step. By comparing the target with the middle element, you determine if the target lies in the left or right half.
=======
- Exploits the sorted property of an array to reduce the search space by half in each step. 
- By comparing the target with the middle element, we can eliminate the half where the target cannot possibly exist.
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## ⚡ Quick Recall (VERY IMPORTANT)

<<<<<<< HEAD
Maintain `low` and `high` pointers. While `low <= high`, calculate `mid = low + (high - low) // 2` and shrink the range based on `nums[mid]` vs `target`.
=======
- Sorted Array? -> `mid = left + (right - left) // 2`. If `arr[mid] < target`, `left = mid + 1`, else `right = mid - 1`.
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Approach

### Brute Force
<<<<<<< HEAD
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
=======
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
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Code (Python)

```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        if not nums:
            return -1
            
        left, right = 0, len(nums) - 1
        
<<<<<<< HEAD
        while low <= high:
            # Prevent potential integer overflow (though not an issue in Python)
            mid = low + (high - low) // 2
=======
        while left <= right:
            mid = left + (right - left) // 2
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b
            
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

<<<<<<< HEAD
| Step | low | high | mid | nums[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 3 | `3 < 9`, so `low = mid + 1 = 3`. |
| 2 | 3 | 5 | 4 | 9 | `9 == 9`, Target found! Return index 4. |
=======
| Step | Left | Right | Mid | `nums[mid]` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 3 | $3 < 9$, so `left = 2 + 1 = 3` |
| 2 | 3 | 5 | 4 | 9 | $9 == 9$, Target found at index 4 |
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Edge Cases

<<<<<<< HEAD
- **Empty Array:** `nums = []`. Loop won't execute, returns -1.
- **Single Element:** `nums = [5], target = 5`. `low=0, high=0, mid=0`. Found.
- **Target Not Present:** `nums = [1, 3], target = 2`. `low` will eventually exceed `high`.
- **Target at Boundaries:** Target is at index `0` or `len-1`.
=======
- **Empty Array:** Should return -1 immediately.
- **Single Element:** Check if `nums[0]` is the target.
- **Target at Boundaries:** Target is the first or last element.
- **Target Not Present:** `left` will eventually exceed `right`.
- **Large Arrays:** Ensure `mid` calculation doesn't overflow (though Python handles large integers, this is a standard interview point).
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Mistakes

<<<<<<< HEAD
- **Infinite Loop:** Using `while low < high` instead of `low <= high` (misses the last element).
- **Integer Overflow:** Using `(low + high) // 2` in languages with fixed-size integers (use `low + (high - low) // 2`).
- **Incorrect Updates:** Doing `low = mid` or `high = mid` instead of `mid + 1` / `mid - 1` can cause infinite loops.
- **Unsorted Input:** Binary search fails if the array is not sorted.
- **User Mistake:** No specific note provided.
=======
- **CRITICAL:** Forgot to handle empty array (`if not nums: return -1`).
- **Off-by-one:** Using `while left < right` instead of `while left <= right`.
- **Mid Overflow:** Using `(left + right) // 2` instead of `left + (right - left) // 2`.
- **Incorrect Update:** Forgetting the `+1` or `-1` when updating `left` or `right`.
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Complexity

<<<<<<< HEAD
Time: O(log N) → Search space is halved in every iteration.  
Space: O(1) → Iterative approach uses only a few variables.
=======
Time: $O(\log n)$ → The search space is halved in every iteration.  
Space: $O(1)$ → Only a constant amount of extra space is used for pointers.
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
<<<<<<< HEAD
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
=======
- [First and Last Position of Element](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
## Tags and Properties
<<<<<<< HEAD

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
=======
- #dsa #important #revisit #blind75
- #binary-search [[Binary Search]], #searching [[Searching]], #sorting [[Sorting]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [LeetCode Binary Search](https://leetcode.com/problems/binary-search/)
>>>>>>> bf1da7fef4f9f006277cbae8e267bbe394aa593b

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
