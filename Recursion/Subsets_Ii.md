---
created: 2026-07-17
revisions:
  - 2026-07-19
  - 2026-07-24
  - 2026-08-01
  - 2026-08-16
---

# Subsets Ii

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #backtracking [[Backtracking]], #recursion [[Recursion]], #sorting [[Sorting]]

## Pattern

Backtracking + Sorting for duplicate elimination

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Sort the input array to group duplicate elements. In recursion at index `ind`, choose any element `i` from `ind` to `n-1`. Skip duplicate elements at the *current* decision level by checking if `i > ind` and `nums[i] == nums[i-1]`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort first. Loop `i` from `ind` to `n-1`. Skip duplicates with `if i > ind and nums[i] == nums[i-1]: continue` to ensure a duplicate element is only picked once as the first choice at that recursion level.

---

## Approach

### Brute Force
- Generate all subset combinations (power set) using backtracking, insert into a set to remove duplicates, and convert back to list.
- Time Complexity: O(2^N * N log N)

### Better
- Count frequencies of each unique element. Perform backtracking using unique elements and branching based on their count options (0 to count).
- Time Complexity: O(2^N)

### Optimal
- Sort the array. Recurse by starting a loop from `ind` to `n-1`. For any iteration, if `nums[i]` is a duplicate of `nums[i-1]` and `i` is not the first index of the loop (`i > ind`), skip to avoid generating duplicate branches.
- Time Complexity: O(2^N * N)

---

## Code (Python)

```python
class Solution:
    def subsetsWithDup(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()  # Crucial to group duplicates together

        def backtrack(ind: int, path: list[int]):
            res.append(list(path))  # Add current subset copy

            for i in range(ind, len(nums)):
                # If current element is duplicate of previous, and not the first in this recursion level
                if i > ind and nums[i] == nums[i-1]:
                    continue
                path.append(nums[i])
                backtrack(i + 1, path)  # Recurse with next index
                path.pop()  # Backtrack

        backtrack(0, [])
        return res
```

---

## Dry Run (Smart Example)

Input: `nums = [1, 2, 2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `ind=0, path=[]` | Add `[]` to `res`. Loop `i` starts. `i=0`: push `1`, path=`[1]`, recurse to `ind=1`. |
| 2 | `ind=1, path=[1]` | Add `[1]` to `res`. Loop `i` starts. `i=1`: push `2`, path=`[1,2]`, recurse to `ind=2`. |
| 3 | `ind=2, path=[1,2]` | Add `[1,2]` to `res`. Loop `i` starts. `i=2`: push `2`, path=`[1,2,2]`, recurse to `ind=3`. |
| 4 | `ind=3, path=[1,2,2]` | Add `[1,2,2]` to `res`. Recursion base case reached. Return. Backtrack: pop `2`, pop `2`. |
| 5 | `ind=1, i=2` | In `ind=1` frame, `i` increments to 2. Since `i > ind` (2 > 1) and `nums[2] == nums[1]`, skip. Return. Backtrack: pop `1`. |
| 6 | `ind=0, i=1` | In `ind=0` frame, `i` increments to 1. Push `2`, path=`[2]`, recurse to `ind=2`. Add `[2]` to `res`. |
| 7 | `ind=2, path=[2]` | Loop `i` starts. `i=2`: push `2`, path=`[2,2]`, recurse to `ind=3`. Add `[2,2]` to `res`. Return. Backtrack: pop `2`, pop `2`. |
| 8 | `ind=0, i=2` | In `ind=0` frame, `i` increments to 2. Since `i > ind` (2 > 0) and `nums[2] == nums[1]`, skip. Done. |

---

## Edge Cases

- **Empty input array:** Handled correctly, returns `[[]]`.
- **All elements identical (`[2, 2, 2]`):** Correctly skips duplicate branches, returns subsets of lengths 0, 1, 2, and 3.
- **No duplicates (`[1, 2, 3]`):** Behaves like normal subset generation, producing all 8 combinations.
- **Negative numbers present:** Sorting handles negative integers correctly, placing them adjacently.

---

## Mistakes

- **Forgetting to sort:** Without sorting, duplicates are not adjacent, and the `nums[i] == nums[i-1]` check fails.
- **Using `i > 0` instead of `i > ind`:** `i > 0` globally prevents picking duplicates at any level. `i > ind` only prevents picking duplicates at the *current* level of decision-making while still allowing the first duplicate to be chosen.

---

## Complexity

Time: O(2^N * N) → There are 2^N subsets, and copying each subset to the result takes O(N) time.
Space: O(N) → Auxiliary stack space for recursion has a maximum depth of N, and the path list takes O(N) space.

---

## Similar Problems

- [Subsets](https://leetcode.com/problems/subsets/) - Medium
- [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/) - Medium
- [Permutations II](https://leetcode.com/problems/permutations-ii/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #backtracking #recursion #sorting [[Backtracking]] [[Recursion]] [[Sorting]]
- **Problem Link:** [LeetCode - Subsets II](https://leetcode.com/problems/subsets-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-19)
- [ ] Day 7 Revision (2026-07-24)
- [ ] Day 15 Revision (2026-08-01)
- [ ] Day 30 Revision (2026-08-16)
