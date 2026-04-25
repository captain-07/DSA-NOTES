---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Kadane'S Algorithm

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #GoldmanSachs #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]], #dynamicprogramming [[Dynamic Programming]], #greedy [[Greedy]]

## Pattern

Local Max vs. Global Max (Dynamic Programming)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The maximum subarray sum ending at index `i` is either the element `nums[i]` itself or the sum of `nums[i]` and the maximum subarray sum ending at `i-1`. We carry forward the previous sum only if it's positive.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Decide at every step: "Should I start a new subarray here, or continue the previous one?"  
`current_max = max(num, current_max + num)`

---

## Approach

### Brute Force
- Check every possible subarray sum using nested loops.
- Time: $O(N^2)$ or $O(N^3)$ | Space: $O(1)$

### Better
- Prefix sums to calculate subarray totals faster, but still requires $O(N^2)$ to check all pairs.
- Time: $O(N^2)$ | Space: $O(N)$

### Optimal
- Iterate through the array once.
- Maintain `current_sum` (local max) and `max_so_far` (global max).
- If `current_sum` becomes negative, reset it to 0 (or start fresh from the current element).
- Time: $O(N)$ | Space: $O(1)$

---

## Code (Python)

```python
class Solution:
    def maxSubArray(self, nums: list[int]) -> int:
        # Initialize with first element to handle single-element arrays
        max_so_far = nums[0]
        current_sum = 0
        
        for n in nums:
            # If current_sum is negative, it's better to start fresh
            if current_sum < 0:
                current_sum = 0
            
            current_sum += n
            # Update global maximum
            max_so_far = max(max_so_far, current_sum)
            
        return max_so_far
```

---

## Dry Run (Smart Example)

**Input:** `nums = [-2, 1, -3, 4, -1, 2, 1]`

| Step | Num | `current_sum` | `max_so_far` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | -2 | -2 | -2 | Initial state. |
| 2 | 1 | 1 | 1 | `-2 < 0`, reset to 0 then add 1. |
| 3 | -3 | -2 | 1 | `1 + (-3) = -2`. `max_so_far` stays 1. |
| 4 | 4 | 4 | 4 | `-2 < 0`, reset to 0 then add 4. |
| 5 | -1 | 3 | 4 | `4 + (-1) = 3`. |
| 6 | 2 | 5 | 5 | `3 + 2 = 5`. New global max. |
| 7 | 1 | 6 | 6 | `5 + 1 = 6`. Final max. |

---

## Edge Cases

- **All Negative Numbers:** The algorithm must return the largest single negative number (not 0).
- **Single Element:** Returns the element itself.
- **Large Array:** Ensure no overflow (not an issue in Python).
- **All Positive:** Returns the sum of the entire array.

---

## Mistakes

- **Initializing `max_so_far` to 0:** Fails if all numbers are negative. Initialize to `-infinity` or `nums[0]`.
- **Resetting `current_sum` too late:** Ensure you decide to restart *before* or *at* the point where the prefix sum becomes detrimental.
- **User Mistake:** No specific note provided (ensure this template is used for future revisions).

---

## Complexity

Time: $O(N)$ → Single pass through the array.  
Space: $O(1)$ → Only using two scalar variables.

---

## Similar Problems

- [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) - Medium
- [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) - Easy
- [Maximum Sum Circular Subarray](https://leetcode.com/problems/maximum-sum-circular-subarray/) - Medium
- [K-Concatenation Maximum Sum](https://leetcode.com/problems/k-concatenation-maximum-sum/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #arrays #greedy
  - [[Arrays]] [[Dynamic Programming]] [[Subarray]]
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
