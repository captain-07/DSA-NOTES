---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Maximum Product Subarray In An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #LinkedIn

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #dynamicprogramming [[Dynamic Programming]]
  - #array [[Array]]
  - #kadane [[Kadane's Algorithm]]

---
## Pattern

Dynamic Programming (Dual State Tracking) OR Prefix & Suffix Product Scan

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The presence of **negative numbers** and **zeros** is the challenge. A negative number can turn the smallest product (highly negative) into the largest product (highly positive). Therefore, we must track both the **maximum** and **minimum** products ending at the current position.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Track `curr_max` and `curr_min`. If the current number is negative, **swap** `curr_max` and `curr_min` before calculating the new values.

---

## Approach

### Brute Force
- Check every possible subarray product using nested loops.
- Time: $O(N^2)$ | Space: $O(1)$

### Optimal 1: Modified Kadane (State Tracking)
- Maintain `max_so_far` and `min_so_far`.
- For each number:
  1. If $nums[i] < 0$, swap `max_so_far` and `min_so_far`.
  2. Update `max_so_far = max(nums[i], max_so_far * nums[i])`.
  3. Update `min_so_far = min(nums[i], min_so_far * nums[i])`.
  4. Global result is the max of all `max_so_far` values.

### Optimal 2: Prefix and Suffix Scan
- The maximum product must involve a prefix or a suffix (unless interrupted by zeros).
- Iterate forward to calculate prefix products.
- Iterate backward to calculate suffix products.
- Reset the product to 1 if a zero is encountered.
- The answer is the maximum value seen during both scans.

---

## Code (Python)

```python
class Solution:
    def maxProduct(self, nums: list[int]) -> int:
        if not nums:
            return 0
        
        # Method: Modified Kadane
        res = nums[0]
        cur_max, cur_min = 1, 1
        
        for n in nums:
            # If negative, max becomes min and min becomes max
            if n < 0:
                cur_max, cur_min = cur_min, cur_max
                
            # Compute new candidates
            temp_max = n * cur_max
            temp_min = n * cur_min
            
            # Update states
            cur_max = max(n, temp_max)
            cur_min = min(n, temp_min)
            
            res = max(res, cur_max)
            
        return res
```

---

## Dry Run (Smart Example)

Input: `nums = [2, 3, -2, 4]`

| Step | Num | `cur_max` (before update) | `cur_min` (before update) | Explanation | Result |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 2 | 1 | 1 | `max(2, 2*1) = 2`, `min(2, 2*1) = 2` | 2 |
| 2 | 3 | 2 | 2 | `max(3, 3*2) = 6`, `min(3, 3*2) = 3` | 6 |
| 3 | -2 | 6 | 3 | **Swap (3, 6)**: `max(-2, -2*3) = -2`, `min(-2, -2*6) = -12` | 6 |
| 4 | 4 | -2 | -12 | `max(4, 4*-2) = 4`, `min(4, 4*-12) = -48` | 6 |

---

## Edge Cases

- **Single Element:** `[ -5 ]` -> Returns `-5`.
- **All Negatives:** `[-2, -3, -4]` -> Product of two negatives is positive.
- **Zeros:** `[2, 0, -1]` -> Zeros reset the contiguous product chain.
- **Alternating Signs:** `[1, -2, 3, -4]` -> Tracks how signs flip.

---

## Mistakes

- **Ignoring the Minimum:** Failing to track `cur_min` means you miss the "negative * negative = positive" jump.
- **Zero Handling:** Not resetting or correctly handling zeros in prefix/suffix logic.
- **Initialization:** Initializing `res` to 0 instead of `nums[0]` (fails on all-negative arrays).
- **User Mistake:** No specific note provided (ensure structured revision notes are created).

---

## Complexity

Time: $O(N)$ → Single pass through the array.  
Space: $O(1)$ → Only a few variables used regardless of input size.

---

## Similar Problems

- [Maximum Subarray (Sum)](https://leetcode.com/problems/maximum-subarray/) - Medium
- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) - Medium
- [House Robber](https://leetcode.com/problems/house-robber/) - Medium
- [Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/) - Medium

---

## Tags and Properties
- #dsa #important #revisit
- #dynamicprogramming [[Dynamic Programming]]
- #array [[Array]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [LeetCode - Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
