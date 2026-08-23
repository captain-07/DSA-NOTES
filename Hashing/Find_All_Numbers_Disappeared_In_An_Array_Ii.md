---
created: 2026-08-23
revisions:
  - 2026-08-25
  - 2026-08-30
  - 2026-09-07
  - 2026-09-22
---

# Find All Numbers Disappeared In An Array Ii

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #arrays [[Arrays]], #cyclesort [[Cycle Sort]], #hashmap [[HashMap]]

## Pattern
In-place Index Hashing (Negative Marking) or Cycle Sort

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Use the array itself as a hash table. Since numbers are in the range $[1, n]$, map each value `val` to the index `abs(val) - 1` and negate the value at that index to mark it as seen. Any index remaining positive represents a missing number.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Treat array values as indices. Iterate and negate `nums[abs(x) - 1]`. Indices with positive values at the end are your missing numbers (index + 1).

---

## Approach

### Brute Force
- Store all elements in a hash set, then loop from $1$ to $n$ and check if each number exists in the set.
- Time: $O(N)$ | Space: $O(N)$

### Better
- Sort the array first, then scan linearly to identify gaps between consecutive elements.
- Time: $O(N \log N)$ | Space: $O(1)$ (or $O(N)$ depending on sorting algorithm)

### Optimal
- **Step 1:** Iterate through the array. For each number `x`, find its target index `idx = abs(x) - 1`.
- **Step 2:** If `nums[idx]` is positive, multiply it by `-1` to mark it.
- **Step 3:** Iterate again. If `nums[i]` is positive, add `i + 1` to the result list.
- Time: $O(N)$ | Space: $O(1)$ auxiliary space.

---

## Code (Python)

```python
class Solution:
    def findDisappearedNumbers(self, nums: list[int]) -> list[int]:
        # Step 1: Mark visited indices by negating values
        for num in nums:
            idx = abs(num) - 1
            if nums[idx] > 0:
                nums[idx] = -nums[idx]

        # Step 2: Collect all indices that remain positive
        return [i + 1 for i, val in enumerate(nums) if val > 0]
```

---

## Dry Run (Smart Example)

Input: `nums = [4, 3, 2, 7, 8, 2, 3, 1]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `num = 4`, `idx = 3` | Negate `nums[3]` -> `nums` becomes `[4, 3, 2, -7, 8, 2, 3, 1]` |
| 2 | `num = 3`, `idx = 2` | Negate `nums[2]` -> `nums` becomes `[4, 3, -2, -7, 8, 2, 3, 1]` |
| 3 | `num = -2`, `idx = 1` | Negate `nums[1]` -> `nums` becomes `[4, -3, -2, -7, 8, 2, 3, 1]` |
| 4 | `num = -7`, `idx = 6` | Negate `nums[6]` -> `nums` becomes `[4, -3, -2, -7, 8, 2, -3, 1]` |
| 5 | `num = 8`, `idx = 7` | Negate `nums[7]` -> `nums` becomes `[4, -3, -2, -7, 8, 2, -3, -1]` |
| 6 | `num = 2`, `idx = 1` | `nums[1]` is already negative (`-3`), do nothing. |
| 7 | `num = -3`, `idx = 2` | `nums[2]` is already negative (`-2`), do nothing. |
| 8 | `num = -1`, `idx = 0` | Negate `nums[0]` -> `nums` becomes `[-4, -3, -2, -7, 8, 2, -3, -1]` |
| 9 | `Collect` | Indices `4` and `5` have positive values (`8` and `2`). Missing: `[5, 6]`. |

---

## Edge Cases

- **All numbers present:** `[1, 2, 3, 4]` -> returns `[]`.
- **All duplicates of one number:** `[1, 1, 1, 1]` -> returns `[2, 3, 4]`.
- **Minimum length array:** `[1]` or `[2, 2]` -> handles boundary correctly.

---

## Mistakes

- *No specific note provided.* (User mistake)
- Modifying index mapping without using absolute value (`abs(num)`), leading to out-of-bounds or incorrect indexing once elements are negated.
- Forgetting that the output array does not count toward the $O(1)$ auxiliary space complexity.

---

## Complexity

Time: O(N) → Two linear scans of the array of size N.
Space: O(1) → In-place negation requires no auxiliary data structures.

---

## Similar Problems

- [Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/) - Medium
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) - Medium
- [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) - Hard

---

## Tags and Properties
  - #dsa #important #revisit
  - #arrays [[Arrays]] #cyclesort [[Cycle Sort]]
  - **Problem Link:** [LeetCode - Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-08-25)
- [ ] Day 7 Revision (2026-08-30)
- [ ] Day 15 Revision (2026-09-07)
- [ ] Day 30 Revision (2026-09-22)
