---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Binary Search

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Meta #Apple #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #searching [[Searching]], #divideandconquer [[Divide and Conquer]], #arrays [[Arrays]]

## Pattern

Decrease and Conquer (Logarithmic Search Space Reduction)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

- Exploits the property of **sorted data** to eliminate half of the remaining search space in each step.
- Compare the target with the middle element: if not equal, discard the half where the target cannot possibly exist.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- `while low <= high`: Calculate `mid = low + (high - low) // 2`. 
- If `arr[mid] < target`, `low = mid + 1`. Else `high = mid - 1`.

---

## Approach

### Brute Force
- Linear Search: Iterate through every element until the target is found or the end is reached.
- Time: O(N)

### Better
- N/A (Binary Search is the standard optimized approach for sorted arrays).

### Optimal
- **Iterative Binary Search**:
  1. Initialize `low = 0`, `high = len(arr) - 1`.
  2. While `low <= high`:
     - `mid = low + (high - low) // 2` (Prevents overflow in some languages).
     - If `arr[mid] == target`, return `mid`.
     - If `arr[mid] < target`, move `low` to `mid + 1`.
     - If `arr[mid] > target`, move `high` to `mid - 1`.
  3. Return -1 if not found.

---

## Code (Python)

```python
def binary_search(nums, target):
    low, high = 0, len(nums) - 1
    
    while low <= high:
        # Prevents (low + high) overflow
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

**Input:** `nums = [-1, 0, 3, 5, 9, 12], target = 9`

| Step | Variables (low, high, mid) | Explanation |
| :--- | :--- | :--- |
| 1 | low=0, high=5, mid=2 | nums[2]=3 < 9. Target must be in the right half. Move low to 3. |
| 2 | low=3, high=5, mid=4 | nums[4]=9 == 9. Target found at index 4. |
| 3 | - | Return 4. |

---

## Edge Cases

- **Target not in array:** Loop finishes (`low > high`), returns -1.
- **Single element array:** Correctly checks `low == high`.
- **Empty array:** `low=0, high=-1`, loop never starts, returns -1.
- **Duplicates:** Standard BS returns *any* index of target. (Use bisect_left/right for first/last occurrence).

---

## Mistakes

- Using `while low < high` (misses the last element when `low == high`).
- Incorrectly updating pointers: `low = mid` or `high = mid` (can cause infinite loops).
- Forgeting the array MUST be sorted.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Search space is halved in every iteration.  
Space: O(1) → Constant space for iterative; O(log N) for recursive due to call stack.

---

## Similar Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy
- [First and Last Position of Element](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #searching #logarithmic  
  - [[Binary Search]] [[Searching Algorithms]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Binary Search](https://leetcode.com/problems/binary-search/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
