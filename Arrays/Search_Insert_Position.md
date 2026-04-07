---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Search Insert Position

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Apple #Adobe #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #arrays [[Arrays]]

## Pattern

Binary Search (Sorted Array / Insertion Logic)

---
## Difficulty

Easy / #easy

---

## ⚡ Key Idea (Core Insight)

Since the array is sorted, we use **Binary Search**. The crucial insight is that if the target is not found, the `left` pointer will naturally converge to the index where the target *should* be inserted to maintain order.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Standard Binary Search: If `nums[mid] == target`, return `mid`. If the loop finishes without a match, **return `left`**.

---

## Approach

### Brute Force
- Iterate through the array linearly and return the index of the first element $\ge$ target. If none found, return `len(nums)`.
- **Time Complexity:** $O(N)$

### Optimal
- Use a **Low/High** (or Left/Right) pointer approach.
- Calculate `mid = (left + right) // 2`.
- Adjust pointers:
    1. If `nums[mid] == target`, target found at `mid`.
    2. If `nums[mid] < target`, move `left = mid + 1`.
    3. If `nums[mid] > target`, move `right = mid - 1`.
- If the loop exits, `left` represents the smallest index such that `nums[left] > target`.
- **Time Complexity:** $O(\log N)$

---

## Code (Python)

```python
def searchInsert(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
            
    # If not found, 'left' is the insertion index
    return left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 3, 5, 6]`, `target = 2`

| Step | left | right | mid | nums[mid] | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 3 | 1 | 3 | `3 > 2` → `right = mid - 1` (0) |
| 2 | 0 | 0 | 0 | 1 | `1 < 2` → `left = mid + 1` (1) |
| 3 | 1 | 0 | - | - | `left > right` → Loop Ends |
| **Result** | **1** | - | - | - | **Return left (1)** |

---

## Edge Cases

- **Target smaller than all elements:** `left` remains 0, returns 0.
- **Target larger than all elements:** `left` moves past `len(nums) - 1`, returns `len(nums)`.
- **Target exists in array:** Returns the exact index.
- **Empty array:** Loop doesn't run, returns `left` (0).
- **Single element array:** Correctly handles insert before or after.

---

## Mistakes

- **Insertion Logic:** Forgetting that `left` is the correct index after the loop fails. Some try to return `mid` or `right`, which is incorrect for boundary cases.
- **Overflow:** Using `(left + right) // 2` instead of `left + (right - left) // 2` (relevant in languages with fixed integer sizes).
- **Boundary:** Not using `left <= right` in the while condition, leading to missing the last possible index.

---

## Complexity

Time: $O(\log N)$ → Binary search halves the search space in each iteration.  
Space: $O(1)$ → Constant space used for pointers.

---

## Similar Problems

- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Easy
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Binary Search](https://leetcode.com/problems/binary-search/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #binarysearch #arrays #easy-win
  - [[Binary Search]] [[Arrays]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [Search Insert Position - LeetCode](https://leetcode.com/problems/search-insert-position/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
