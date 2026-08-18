---
created: 2026-07-17
revisions:
  - 2026-07-19
  - 2026-07-24
  - 2026-08-01
  - 2026-08-16
---

# Subsets II

---

## Metadata & Placement Tags

- **Target Companies:** #Amazon #Facebook #Google #Microsoft #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #backtracking [[Backtracking]], #sorting [[Sorting]], #recursion [[Recursion]]

## Pattern

Backtracking + Sorting

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

To avoid duplicate subsets, sort the array first. In the backtracking loop, skip duplicate elements at the current recursion level. The condition `i > ind` ensures we only skip duplicates *horizontally* (same level), but still allows them *vertically* (nested levels).

---
## ⚡ Quick Recall (VERY IMPORTANT)

Sort first. Backtrack with loop: skip if `i > ind` and `nums[i] == nums[i-1]`.

---
## Approach

### Brute Force
- Generate all possible subsets using standard backtracking, insert them into a hash set to remove duplicates, and convert the set back to a list.
- Time Complexity: O(N * 2^N log(2^N))

### Better
- N/A

### Optimal
1. Sort the input array `nums`.
2. Implement recursive helper `backtrack(ind, path)`.
3. Add a copy of `path` to results at the start of each call.
4. Iterate `i` from `ind` to `len(nums) - 1`.
5. If `i > ind` and `nums[i] == nums[i-1]`, skip the iteration.
6. Push `nums[i]` to `path`, recurse with `backtrack(i + 1, path)`, then pop `nums[i]`.

---
## Code (Python)

```python
class Solution:
    def subsetsWithDup(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()  # Crucial to group duplicates
        self.backtrack(0, nums, [], res)
        return res

    def backtrack(self, ind: int, nums: list[int], path: list[int], res: list[list[int]]):
        res.append(list(path))  # Copy path to avoid reference sharing

        for i in range(ind, len(nums)):
            # Skip duplicate elements at the same recursion depth
            if i > ind and nums[i] == nums[i - 1]:
                continue

            path.append(nums[i])
            self.backtrack(i + 1, nums, path, res)
            path.pop()  # Backtrack
```

---
## Dry Run (Smart Example)

Input: `nums = [1, 2, 2]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `ind=0`, `path=[]` | Append `[]` to `res`. Start loop `i` from 0 to 2. |
| 2 | `i=0`, `path=[1]` | Recurse `ind=1`. Append `[1]` to `res`. Start loop `i` from 1 to 2. |
| 3 | `i=1`, `path=[1, 2]` | Recurse `ind=2`. Append `[1, 2]` to `res`. Start loop `i` from 2 to 2. |
| 4 | `i=2`, `path=[1, 2, 2]` | Recurse `ind=3`. Append `[1, 2, 2]` to `res`. Recurse ends. Pop -> `[1, 2]`. |
| 5 | `i=2`, `path=[1]` | Back to `ind=1` level. Loop `i=2`. Skipped because `i > ind` (2 > 1) and `nums[2] == nums[1]` (2 == 2). Pop -> `[]`. |
| 6 | `i=1`, `path=[2]` | Back to `ind=0` level. Loop `i=1`. Recurse `ind=2`. Append `[2]` to `res`. Loop `i` from 2 to 2. |
| 7 | `i=2`, `path=[2, 2]` | Recurse `ind=3`. Append `[2, 2]` to `res`. Recurse ends. Pop -> `[2]`. |
| 8 | `i=2`, `path=[]` | Back to `ind=0` level. Loop `i=2`. Skipped because `i > ind` (2 > 0) and `nums[2] == nums[1]` (2 == 2). |

---
## Edge Cases

- **Empty Array (`[]`):** Returns `[[]]` correctly.
- **All Duplicates (`[2, 2, 2]`):** Generates `[[], [2], [2,2], [2,2,2]]` without duplicate arrays.
- **Single Element (`[1]`):** Returns `[[], [1]]`.
- **Negative Elements (`[-1, -1, 2]`):** Handled correctly due to initial sorting.

---
## Mistakes

- **Incorrect check `i > 0` instead of `i > ind`:** Using `i > 0` skips valid duplicates at nested levels (e.g. preventing `[1, 2, 2]` from including the second `2` when the first `2` is already in the subset). `i > ind` ensures we only skip duplicates among sibling branches at the same depth.
- **Forgetting to sort `nums`:** The duplicate-skipping check relies on identical elements being adjacent.
- **Not copying the path list:** Appending `path` directly (e.g., `res.append(path)`) stores references, causing empty lists in the final result.

---
## Complexity

Time: O(N * 2^N) → There are 2^N possible subsets. We copy each subset in O(N) time. Sorting takes O(N log N).
Space: O(N * 2^N) → To store the output list of subsets, plus O(N) recursion stack depth.

---
## Similar Problems

- [Subsets](https://leetcode.com/problems/subsets/) - Medium
- [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/) - Medium
- [Permutations II](https://leetcode.com/problems/permutations-ii/) - Medium

---
## Tags and Properties

- #dsa #important #revisit
- #backtracking [[Backtracking]]
- #sorting [[Sorting]]
- **Revision Date:** 2026-07-17
- **Problem Link:** [Subsets II - LeetCode](https://leetcode.com/problems/subsets-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-07-19)
- [ ] Day 7 Revision (2026-07-24)
- [ ] Day 15 Revision (2026-08-01)
- [ ] Day 30 Revision (2026-08-16)
